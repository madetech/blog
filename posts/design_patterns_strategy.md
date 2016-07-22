## Design Patterns: Strategy

Design patterns are solutions to software design problems that are presented in an almost conceptual way. That is to say, a given design pattern has the potential to be applied to a piece of software written in any number of languages but, at a project level, it's up to the developer to interpret that idea and make it work for them.

In my last post on design patterns, [I discussed the Observer pattern](https://www.madetech.com/blog/design-patterns-observer), which is basically a way to have a class notify other classes (called observers) of a change, without the original class needing to have explicit knowledge of its observers.

In this post, I'll be discussing the Strategy pattern, another of the behavioural design patterns. Since most of the projects we work on are written using Ruby, the examples here reflect that.

##Problem:
Using a video game, Overwatch, as an example (because I've been playing a lot of it recently), let's say you have a Player object, and it has several attributes, such as PrimaryAbility, SecondaryAbility and UltimateAbility, that will be used throught the game.

People playing the game have the choice of 21 different characters to play as, and each of them have different values associated to those three attributes, so we need to be able to efficiently map those values to the Player object each time they select a character (which can happen several times during a session).

##Solution:
Without thinking about it too much, it might be tempting to steam ahead and layout a Player object that looks like this:

```
class Player do
  def initialize(character_name)
    @character_name = character_name
  end
  ...

  def primary_ability
    if @character_name == 'D.Va'
      'Boosters'
    elsif @character_name == 'Lucio'
      'Crossfade'
    elsif @character_name == 'Reaper'
      'Wraith Form'
    ...
    end
  end

  def secondary_ability
    if @character_name == 'D.Va'
      'Defense Matrix'
    elsif @character_name == 'Lucio'
      'Amp It Up'
    elsif @character_name == 'Reaper'
      'Shadow Step'
    ...
    end
  end

  def ultimate_ability
    if @character_name == 'D.Va'
      'Self-Destruct'
    elsif @character_name == 'Lucio'
      'Sound Barrier'
    elsif @character_name == 'Reaper'
      'Death Blossom'
    ...
    end
  end
end

player = Player.new('Lucio')
```

Obviously, this already looks incredibly unweildy, and I've only listed three characters. Expand this out to all 21 characters and every attribute unique to each of them (speed, health, shields etc), and you'd have something that would make anyone cry. Additionally, if Blizzard were to add a new character to the game, they'd have the unenviable task of needing to go through and modify each of those if/else blocks to accommodate said character's values. There must be a better way, right? RIGHT!




