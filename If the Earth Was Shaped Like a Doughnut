from vpython import scene, ring, sphere, local_light, canvas, vector, textures, color, rate # imports the relevant functions from vpython
from math import sin, cos, copysign # import relevant functions from math

# scene = canvas() # allows the scene to be redrawn without restarting the kernel
scene.lights = [] # gets rid of the default lights
scene.ambient = color.gray(0.07) # Makes the ambient lighting much dimmer
sim_speed = 0.8 # the speed of the simulation
dt = 0.04 # time step
sim_rate = sim_speed/dt # sets how many animations per second will be created
t = 0 # starts t out at 0
s = 0.5 # scales everything porportionally, it's useful for graphics purposes
scene.range = 6*s # makes the camera not be super zoomed out
orbit_dis = 200*s # orbital distance of the earth
spin_speed = 6

doughnut_earth = ring(pos = vector(0, 0, -orbit_dis), axis = vector(0,1,0.6), radius = 2.5*s, thickness = 1*s, texture = textures.earth, opacity=0.999) # creates the earth
doughnut_moon = ring(pos = vector(0, 0, -orbit_dis), axis = vector(0,1,0.6), radius = 0.5*s, thickness = 0.25*s, texture = textures.rough, opacity=0.999) # creates the moon
sun = sphere(pos = vector(0, 0, 0), radius = 20*s, emissive = True) # creates a spherical sun
# sun = ring(pos = vector(0, 0, 0), axis = vector(0,1,0), radius = 10*s, thickness = 6*s, emissive = True) # creates a doughnut-shaped sun
local_light(pos = vector(0, 0, 0), color=color.white) # makes the sun give light
local_light(pos = vector(0, 0, 0), color=color.gray(0.3)) # makes the sun slightly brighter

def f():
    return doughnut_earth.pos + vector(0.5*sin(t)*s, 0, 0) # the camera follows the position of the earth

while True:
    rate(sim_rate) # the better your computer is, the higher this number can be
    doughnut_earth.pos = vector(orbit_dis*sin(t)*s, 0, orbit_dis*cos(t)*s) # makes the earth move in it's orbit
    doughnut_moon.pos = doughnut_earth.pos + vector(3.5*(copysign(1,sin(t))*sin(t)*sin(t)+sin(t))*s, (7*cos(t)*sin(t)-0.5)*s, 0)# makes the moon orbit the earth in a cool way
    doughnut_earth.rotate(angle = spin_speed*dt) # rotates the earth
    doughnut_moon.rotate(angle = spin_speed*dt) # rotates the moon
    scene.camera.follow(f) # has the camera follow the earth
    t += dt # advances time
