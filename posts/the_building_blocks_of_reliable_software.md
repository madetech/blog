The Building blocks of reliable software
-----------------------------------------

  - Introduction
  - State as a separation of concerns
  - Single public method and it's anatomy
  - Hashes as the transport mechanism
  - Principle of least surprise
  - Easy testing
  - Show me

Introduction
-------------
  When solving requirements for a system, you should extract specific roles out into service objects.

  The lazy path is to solve problems directly where you encounter them such as in the controller, model or view (given you are using MVC of course).

  You are missing a 'code seam' that you can hook into to get the desired functionality from.

  Instead you should create very simple, small objects (generally less than a hundred lines), with verbose names describing exactly what problem
  they solve.  In Ruby these are known as PORO's.

State as a separation of concerns
---------------------------------
  A referentially transparent (or pure) function will always return the same output given the same input.

  These are considered dependable because they are not affected by the outside world beyond what they are given as arguments.

  In this setup I propose having atleast a pair objects for accomplishing tasks.
  One which deals with stateful things and the other operates only on it's arguments.

  I will call non-stateful object a Value Object.  The stateful object is a Service Object.

  The value object exists solely to represent the data needed by the stateful object.  It acts as a filter which transforms the shape of the data.
  In a perfect world your data would conform to your program exactly meaning that you have to write almost no code to utilise it.
  This is rarely the case though.

  Stateful objects coordinate actions like writing to a database, sending emails, uploading csv's and all those other volatile things which are undependable might fail.  We need to separate the dependable from the potentially volatile, and the likely to change from the more static code.

  One could argue that the stateless object may change more frequently due to changing requirements, where the stateful object is less likely to.

  In other words, if you were sending an email, the means by which you do this is less likely to change than the data contained within the email over
  a period of time.

Single public method and it's anatomy
-------------------------------------
  Apart from the constructor, there should be only one public method that you can call.
  This method is special and should be comprised of only methods that you have defined.

  It should be a sequence of steps and by simply reading it you should be able to understand everything that the object does.
  Notice that below every method sits at the same level of abstraction.  A layer of abstraction that we have defined ourselves in plain English.

  Good

    def signup_employee
      find_or_create_user
      set_user_as_employee

      notify_via_email
    end

  Bad

    def signup_employee
      find_or_create_user
      set_user_as_employee

      mail('foo@example.com', 'Welcome new employee')
    end

  The mail method above is an abstraction that sits at a lower level than the rest of the methods.
  This applies to both the value objects that are instantiated in the service object and the service object itself.
  In fact I would advise that all methods you write adhere to this.  Adopting this as a discipline will lead to more cohesive code.

Hashes as the transport mechanism
----------------------------------
  Hashes/Maps are primitives that are composed of keys and values and are perfect for packaging up data to be sent to another object.
  They are descriptive enough to make sense on their own just by reading the contents.

  I instantiate both the service objects and value objects with hashes.

  A benefit of using hashes is that you sidestep ordering complexity that you get with positional arguments.
  It does not matter what the order of the contents of your hash is as they are referenced explicitly by key.

  Always prefer to use the .fetch method over [ for accessing values that you expect to be present in your hash.
  This is important because it will throw a key not found error instead of having a nil value percolate through your program undetected.

The Principle of Least Surprise
--------------------------------
  Be weary of writing fancy code.

  Even if it saves you from writing an extra line or two.  It may not be worth it in the long run.

  Write boring, predictable, simplified code.  Write it as if a 5 year old was going to inherit the code base from you.
  Long descriptive names and no abbreviations are the law.

  You will be surprised how hard a piece of code may become to understand after 2 months of not working on it.

  If something could be given a name, do it. first_name is much more intention revealing than person[0] even if the method looks like this:

  def first_name
    person[0]
  end

  You could argue that person[0] is less code but first_name has more meaning and is far superior.

Easy testing
-------------
  When testing these objects, you only assert the outcome of the one public method that the object has.

  With the service object / value object pair testing becomes much easier.
  For testing the value object it need simply be instantiated with a hash of parameters to assert that it has transformed the data into
  the values you require for your service object.  This type of test will be fast and isolated.

  Testing the service object itself has also become easier as there is less setup required and it's been untangled from the data it needs.
  I have no problem with stubs and mocks for testing this at the unit level.

Show me
--------

The Sateful Service Object
--------------------------

  class CaptureUserPdf
    def initialize(params)
      @user = params.fetch(:user)
    end

    def run
      write_pdf
      mark_as_exported
    end

    private

    def mark_as_exported
      @user.mark_as_exported
    end

    def write_pdf
      SomePdfClass.new.write(pdf_user)
    end

    def pdf_user
      PdfUser.new(@user).to_pdf
    end
  end

The Non-Sateful Value Object
-----------------------------

  class PdfUser
    def initialize(params)
      @user = params.fetch(:user)
    end

    def to_pdf
      {
        name:   name,
        status: status
      }
    end

    private

    def name
      @user.name.capitalize
    end

    def status
      return 'manager' if @user.roles.include?(:manager?)

      'worker'
    end
  end
