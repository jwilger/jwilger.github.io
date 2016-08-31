---
title: "Portal Adventure: Implementing Commands"
excerpt: >

  This is the second post in an ongoing series in which I talk about the
  development of "Portal Adventure", a text-based adventure game that my
  10-year-old son and I are writing in order to help him learn about
  programming. **See other posts in this series:**
  [1](/2015/12/07/Portal-Adventure-Session-One.html)

---

Yesterday, Lachlan and I finally got a chance to sit down for a little
while and work on our game a bit more. As I mentioned in [my previous
post in this series][post-1], we left off with the ability to launch the
program, which outputs a description of the character's starting
location and then immediately exits. The next feature we are implementing is
the ability for the player to issue the `look` and `quit` commands.

In our code from last time, we created a `Universe` object that
ultimately holds the state of the running game, and the command-line
script invokes the `Universe#run` method to set things in action. We
also inject a `PlayerInterface` object into the `Universe`, which allows
the game to send its output to the user and, eventually, to receive
input *from* the user.

At this point, our `Universe#run` method looks like this:

```ruby
def run
  active_character.inspect_location(tell: player_interface)
end
```

And the specs covering it:

```ruby
RSpec.describe PortalAdventure::Universe do
  subject {
    described_class.new(player_interface: player_interface,
                        starting_location: starting_location,
                        default_character: default_character)
  }

  let(:player_interface) {
    instance_double('PortalAdventure::PlayerInterface',
                    handle_location_description: nil)
  }

  let(:starting_location) { instance_double('PortalAdventure::Location') }

  let(:room_description) { "You find yourself in a vast, empty space." }

  let(:first_player_character) {
    instance_double('PortalAdventure::PlayerCharacter', 
                    inspect_location: nil)
  }

  let(:default_character) { ->(location:) { first_player_character } }

  describe '#run' do
    it 'describes the first room to the player' do
      allow(first_player_character).to receive(:inspect_location) do |args|
        args[:tell].handle_location_description room_description
      end

      subject.run
      expect(player_interface).to have_received(:handle_location_description)
        .with(room_description)
    end
  end
end
```

Before we even got into writing any code to implement command input, I
realized I didn't really care for that spec on the `#run` method. I
*think* that it must have evolved from something else—possibly a version
of the code before we introduced the `PlayerInterface` and we were just
hitting `STDOUT` directly—but its current form is hiding the signal in a
bunch of noise. All we really want to know here is that it tells the
active character to inspect its current location, and that it provides a
callback object along with that message. I rewrote that spec as such:

```ruby
#...
describe '#run' do
  it 'tells the active character to inspect its location' do
    subject.run
    expect(first_player_character).to have_received(:inspect_location)
      .with(tell: player_interface)
  end
end
```

Much simpler! (Note that I have [RSpec configured to verify
doubles][rspec-verify-doubles], so that it will complain if, for
example, the `PlayerCharacter` class does not actually implement the
`#inspect_location` instance method in the way that it is used here.)

With that change out of the way, I added the next spec to describe our
`#run` method:

```ruby
it 'tells the player interface to process the next command' do
  subject.run
  expect(player_interface).to have_received(:process_next_command)
end
```

This is simplistic, and it should be immediately obvious (to those of us
with experience) that this won't be sufficient to deal with setting up a
program loop that processes multiple commands or to tell us what to
actually *do* with those commands. It turns out that  sometimes the
small steps we need to take while teaching a beginner are a good
reminder to the rest of us that those same small steps can help us
reason about a problem without having to hold the entire solution in our
heads at once.

The truth is, I *did* first start by trying to reason about how the main
loop of the program might be written to process commands and know when
to tell the player character to act versus knowing when to exit the
game, but there were a lot of different possibilities there. I was
floundering a bit and realized I was also quickly losing Lachlan's
attention.  Pausing for a moment I realized that—while we may
*eventually* need to deal with that problem—our immediate need was to
process even a *single* command. If we focused on that first, we could
make some visible forward progress and may also learn a bit more about
what kind of things we will need in order to process multiple commands
in a loop. So, the new spec above is what we decided the next smallest
step was that we could take.

At this point, I ran the specs, and we got an error message about the
`PlayerInterface` class not implementing the `#process_next_command`
method (thanks to that verifying double). So I slid the keyboard over in
front of Lachlan, and said, "Yours." :-)

In our previous session, I had done all of the typing (making sure to be
quite verbose as to *why* I was doing everything), because I wanted to
be sure we made enough progress to have a functional first step. But one
generally learns more by doing rather than watching, so it was time for
Lachlan to start writing the code, too. And yes, I am indoctrinating him
young into the practice of ping-pong pairing. :-)

The main area we focused on today was the concept of message-passing in
object-oriented programming, and how it can be useful to thing of code
such as `object.do_a_thing` as *sending a message*, `do_a_thing`, to the
object as opposed to *calling a method*. Even though you will hear both
interchangeably, the former encourages thinking about objects in terms of
their responsibility rather than allowing them to just become a dumping
ground for methods that seem to use the same set of data.

Due to our short time available last night and the large amount of
explaining I had to do, we didn't make a *ton* of progress; but after a
few passes of the keyboard (at each change in the error message produced
by the tests), we got back to a point where all of our specs were
passing and we could run the program. Of course, because we took the
smallest steps necessary to get that spec to pass, all we ended up with
was a noop method definition in the `PlayerInterface` object:

```ruby
class PlayerInterface
  #...
  def process_next_command
  end
end
```

You can [see the code as of this point in our GitHub
repository][current-commit] for the project.

Next time we will work on getting that new method to actually process
user input and execute the `look` command in the game.

[post-1]: http://johnwilger.com/2015/12/07/Portal-Adventure-Session-One.html
[rspec-verify-doubles]: https://relishapp.com/rspec/rspec-mocks/v/3-4/docs/verifying-doubles
[current-commit]: https://github.com/jwilger/portal_adventure/tree/f144a97204deb9f4c32c7b4fce315e8d40c18838
