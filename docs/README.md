# teched2018-cro2
TechEd 2018 Session Journey For Track CRO2

## Data model for cdsSpaceTrip

### Data Model Structure

The data model is divided into two parts - a base part and an extension:

1. [***FlightModel***](./flightModel.md)  
   The base data model holding those entities needed to represent travel on earth.  This data model uses entities very similar to the data structures used by the ABAP FlightModel
1. [***SpaceModel***](./spaceModel.md)  
   An extension to the base data model holding those entities needed to extend a journey into space

### FlightModel

This data model represents journeys made by airplane on Earth.

Any journey is represented as a series of between 1 and 5 "legs", where each leg represents a direct flight between two airports.

### SpaceModel

This data model extends `FlightModel` and represents journeys that include some aspect of space travel.  Such journeys usually  start or end on Earth.  For the purposes of simplicity, this data model confines itself to travel within our own Solar System.

For instance, if you wish to travel from Earth to the Moon, such as journey would be recorded in two parts:

1. Travelling by airplane from your home city on earth to some spaceport (say, Cape Canaveral)
1. Travelling in some space vehicle from the spaceport to a destination in space

However, traveling on earth is much simpler than travelling in space for the following reasons.  When you travel on earth:

1. You never need to care about which planet you're going to land on - its always the same one from which you took off!
1. If you travel in an airplane, then as all pilots know, take-off is optional, landing is mandatory!  In other words, you are *going* to land back on the surface of the planet.

In space travel though, neither of these assumptions are valid

## Extra Considerations for Space Travel

Navigation on earth is quite straight forward in that for short journeys, the shortest distance between two points is a straight line, and for longer journeys, the shortest distance is a ["Great Circle"](https://en.wikipedia.org/wiki/Great-circle_distance).

In space however, due to the fact that you are moving between the gravitational fields of different planets/moons, all journeys must follow ***elliptical*** paths.

In addition to this, the weight and cost of rocket fuel must be considered.  Consequently, we will always choose the most energy efficient path between two points.  This path will be an ellipse that approximates a [Hohmann Transfer Orbit](https://en.wikipedia.org/wiki/Hohmann_transfer_orbit).

So now, we have some additional factors to consider:

1. The shortest (I.E. cheapest) path between two bodies in space is never a straight line, but always an ellipse.
1. The stages of a space journey do not necessarily start from or end on the surface of a planet.
1. It is entirely possible that our space journey does not intend to land on the destination planet.  
    In this case, gravitational assistance of the destination planet/moon is used to loop around it and then return home.  This is known as a "free return" trajectory.

So, the first question you must answer is this:

> Do I intend to land on the surface of the destination planet?  
>
> Yes or no?

The answer to this question will critically determine the flight path used to get you from Earth to wherever you're going.


### Landing on the Destination Planet/Moon

For example, let's assume you want to repeat the flight path of Apollo 11 and land on the Moon.  Such a journey can be simplified into the following 4 stages (in reality however, the [Apollo 11](https://history.nasa.gov/afj/ap11fj/index.html) flight plan was hugely more complex!):

1. From a spaceport such as Cape Canaveral, launch into a low earth orbit (LEO), then orbit the Earth a couple of times
1. Fire the motors again to enter a transfer orbit that will take you close enough to the Moon to be captured by its gravity (known as trans-lunar injection, or TLI)
1. The TLI brings you close enough to the Moon that you can enter a low lunar orbit.  Here you may orbit the Moon a couple of times.
1. Finally, you descend to the lunar surface

The return flight is the same sequence in reverse:

1. Launch into low lunar orbit
1. Burn the motors a second time to enter a transfer orbit back to Earth.
1. Enter low earth orbit (LEO)
1. Re-enter Earth's atmosphere and descend to the surface


### Not Landing on the Destination Planet/Moon

Alternatively, if you simply want to be a space tourist and loop around your destination planet then immediately return home, your flight path will be somewhat simpler. (This route copies the flight path used by [Apollo 8](https://history.nasa.gov/afj/ap08fj/index.html)).

1. Launch into low earth orbit (LEO), then orbit the Earth a couple of times.
1. Fire the motors again to enter a free-return lunar transfer orbit.  
    This trajectory causes you to be influenced by the Moon's gravity, but not captured by it.  
    In other words, this trajectory is designed to just miss entering low lunar orbit.  Now you will swing around the Moon and return to Earth without needing to fire the motors again (hence the name "free return", since you can return to Earth for free)
1. Enter LEO
1. Re-enter Earth's atmosphere and descend to the surface


