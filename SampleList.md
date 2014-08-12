# General notes

* These are not meant only as demo scenes, but as a sandbox for you to experiment with the behaviours and learn the ins and outs of how UnitySteer agents are composed.  Make sure you at the very least follow the experimentation notes before pressing on.
* Most of these examples will use SteerForTether to ensure that the agent does not wander off too far from the center of the scene.  That’s its sole reason for existing.

# Basic examples

## Wandering

The most basic example: a single agent  wanders aimlessly around the scene while remained tethered between 15 units of (0, 0, 0).

Use this scene to experiment with maximum speed, maximum force, turn time and other AutonomousVehicle properties.

Behaviours used:

- AutonomousVehicle
- SteerForWander
- SteerForTether

## Go For Point

Now things are getting interesting. We have two wanderers on the scene, which will pick a point, move to it, and once they arrive just select a new one.    They do this by using an event handler on the steering behaviour, which triggers when the vehicle has reached its target.

See GoForPointController.cs

There’s two agents on the scene: the green one will approach its target at a constant speed, the yellow one will slow down as it reaches it.

Things to experiment with:

* AutonomousVehicle has two properties that control how quickly it accelerates or decelerates, Acceleration Rate and Deceleration Rate. What happens with the yellow agent if you double the deceleration rate? If you set it to 1?
* What happens with the yellow target if you increase the AutonomousVehicle’s Tick Length? Why?
* What happens if the Turn Time is too high and the target point really close?

Behaviours used:

- AutonomousVehicle
- SteerForPoint

## Neighbor examples

The neighbour examples are a set of scenes meant to demonstrate how the various SteerForNeighbor behaviours interact with each other. I suggest you review them in the following order.

### Neighbors-Alignment

Instantiates a set of agents whose main behaviour is to steer for alignment.  They’ll be created within 10 units of the origin.  Run the scene.

Things to experiment with:

* What happens when you play it? Are all agents moving or do some remain static? Why? (review SteerForAlignment)
* If some agents do remain static, when do they start moving again?
* How is the behaviour affected if you change the Angle value on the prefab’s SteerForNeighborGroup?  What about the Min/Max Radius properties?
* There’s a SteerForForward behaviour on the prefab.  What happens if you enable the behaviour and then play the scene?  
* What happens if you then increase the weight of SteerForForward?
* What happens if you decrease the weight of SteerForNeighborGroup?


# Advanced examples

## Obstacle Avoidance

A large flock of boids will move around a scene while at the same time avoiding scattered capsules, which are treated as spherical obstacles.  If there is a collision with an obstacle, the obstacle will be destroyed and the collision logged. The colliding vehicle will change color.

This is a great scene for experimenting with spherical obstacle avoidance settings and see if they cause more or less collisions and how they change the way voids act.  Some experiments to get you started:

- Increase the number of obstacles on the scene
- Increase or decrease the obstacle’s DetectableObject radius
- Increase the boid prefab’s maximum speed on their AutonomousVehicle
- Increase or decrease the boid prefab’s turn time on their AutonomousVehicle

Main steerings used:

- SteerForSphericalObstacleAvoidance
- SteerForNeighborGroup
- SteerForSeparation
- SteerForCohesion
- SteerForAlignment
- SteerForWander

## Playing Tag

A group of boids will flock around until one of them is designated at a prey.  When that happens, said boid will stop flocking and will start evading the others using SteerForEvasion, and adding some randomness via SteerForWander.  The rest of the behaviours will gradually turn into predators by activating their own pursuit behaviour.

Whichever predator captures the prey will grow slightly fatter and slower.

Main steerings used:

- SteerForNeighborGroup
- SteerForSeparation
- SteerForCohesion
- SteerForAlignment
- SteerForPursuit
- SteerForEvasion
- SteerForWander

There is one main scene, and several demonstrating planar flocking by constraining one axis at a time.

See TagPlayer.cs for the controlling behaviour.
