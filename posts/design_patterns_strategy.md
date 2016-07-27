## Design Patterns: Strategy

Design patterns are solutions to software design problems that are presented in an almost conceptual way. That is to say, a given design pattern has the potential to be applied to a piece of software written in any number of languages but, at a code level, it's up to the developer to interpret that idea and make it work for them.

In my last post on design patterns, [I discussed the Observer pattern](https://www.madetech.com/blog/design-patterns-observer), which is basically a way to have a class notify other classes (called observers) of a change, without the original class needing to have explicit knowledge of its observers.

In this post, I'll be discussing the Strategy pattern, another of the behavioural design patterns. I'm particularly comfortable using the Ruby language, so the examples here will reflect that.

##Problem:
Using a video game, Overwatch, as an example (because I've been playing a lot of it recently), let's say you have a Player class, and it has many attributes, such as primary_ability, secondary_ability and ultimate_ability, that will be used throughout the game.

People playing the game have the choice of 21 different characters to play as, and each of them have different values associated to those three attributes, so we need to be able to efficiently map those values to the Player class each time they select a character. A user is able to switch characters as many times as they like during play, so it's important that this runs as smoothly as possible.

##Solution:
Without thinking about it too much, it might be tempting to plough ahead and create a Player class that looks like this:

```
class Player
  def initialize(character)
    @character = character
  end
  ...

  def primary_ability
    if @character == 'D.Va'
      'Boosters'
    elsif @character == 'Lucio'
      'Crossfade'
    elsif @character == 'Reaper'
      'Wraith Form'
    ...
    end
  end

  def secondary_ability
    if @character == 'D.Va'
      'Defense Matrix'
    elsif @character == 'Lucio'
      'Amp It Up'
    elsif @character == 'Reaper'
      'Shadow Step'
    ...
    end
  end

  def ultimate_ability
    if @character == 'D.Va'
      'Self-Destruct'
    elsif @character == 'Lucio'
      'Sound Barrier'
    elsif @character == 'Reaper'
      'Death Blossom'
    ...
    end
  end
end

player = Player.new('Lucio')
```

Obviously, this already looks incredibly unweildy, and I've only listed three characters. Expand this out to all 21 characters and every attribute unique to each of them (speed, health, shields etc), and you'd have something that would make anyone cry. Additionally, if Blizzard were to add a new character to the game, they'd have the unenviable task of needing to go through and modify each of those if/else blocks to accommodate said character's values. This is a big smell, and a violation of the [open/closed principle](https://en.wikipedia.org/wiki/Open/closed_principle) which states that:

> Software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification.
>
> -- _Bertrand Mayer_

So what we can do is create a series of classes, one per unique character, that defines how each of those characters implement their various abilities:

```
class Dva
  def name
    'D.Va'
  end

  def primary_ability
    'Boosters'
  end

  def secondary_ability
    'Defense Matrix'
  end

  def ultimate_ability
    'Self Destruct'
  end
end

class Lucio
  def name
    'Lucio'
  end

  def primary_ability
    'Crossfade'
  end

  def secondary_ability
    'Amp It Up'
  end

  def ultimate_ability
    'Sound Barrier'
  end
end

class Reaper
  def name
    'Reaper'
  end

  def primary_ability
    'Wraith Form'
  end

  def secondary_ability
    'Shadow Step'
  end

  def ultimate_ability
    'Death Blossom'
  end
end
```
As a side note, if most characters had a common attribute, say jump_height, rather than implement that in each character's class, we could create a Character super class, which each unique character class could then inherit from, and override in exceptional circumstances:

```
class Character
  def jump_height
    0.5
  end
end

class Dva < Character
  # No need to override jump_height
  ...
end

class Genji < Character
  # Allow Genji to jump real high
  def jump_height
    1
  end
end
```

Either way, now, the Player class doesn't need to know about the specifics of how each character implements each of their abilities, we can just pass a particular character to it and be on our way:

```
class Player
  attr_accessor :character

  def initialize(character)
    @character = character
  end

  def character_name
    "Current character: #{character.name}"
  end
  ...
end

player = Player.new(Lucio.new)
player.character_name # 'Current character: Lucio'
player.character.primary_ability # 'Crossfade'
```

Now I'm playing as Lucio, but he's not being particularly effective and I want to switch characters, so all I have to do is call:

```
player.character = Dva.new
player.character_name # 'Current character: D.Va'
player.character.primary_ability # 'Boosters'
```
