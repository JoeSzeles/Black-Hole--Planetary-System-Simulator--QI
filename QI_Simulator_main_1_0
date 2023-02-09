import pygame
import random
import math
import numpy as np
scalefactor = 10000
c = 299792458 # speed of light
G = 6.67430e-11 # gravitational constant
Theta =8.8*10**26
WINDOW_SIZE = (1800, 1000)
DT = 0.003  # time step in seconds
particle_amount=200
black_hole_mass = 40*10**15
black_hole_radius=25
colors = [(random.randint(0, 255), random.randint(0, 255), random.randint(0, 255)) for i in range(particle_amount)]

# Initialize Pygame
pygame.init()

# Set the display
screen = pygame.display.set_mode(WINDOW_SIZE)

# Set the background color
screen.fill((0, 0, 0))

# List to store particles representing the stars
particles = []
black_holes=[]

black_hole = {
    'x': WINDOW_SIZE[0] / 3,
    'y': WINDOW_SIZE[1] / 2,
    'vx': random.uniform(-300, 300),
    'vy': random.uniform(-300, 300),
    'ax': 0,
    'ay': 0,
    'radius':black_hole_radius
}
black_hole_2 = {
    'x': WINDOW_SIZE[0] / 2,
    'y': WINDOW_SIZE[1] / 3,
    'vx': random.uniform(-300, 300),
    'vy': random.uniform(-300, 300),
    'ax': 0,
    'ay': 0,
    'radius':black_hole_radius
}

# Add the black hole
# Add the black holes
black_holes.append(black_hole)
black_holes.append(black_hole_2)

black_hole_x, black_hole_y = WINDOW_SIZE[0]/2, WINDOW_SIZE[1]/2


# Add 100 particles to the list
for i in range(particle_amount):
     pradius = random.uniform(2, 8)
     m_i = random.uniform(2*10**8, 4*10**15)
     particles.append([random.randint(0, 1800), random.randint(0, 1000), random.randint(-10, 10), random.randint(-10, 10), m_i, pradius])

# Create a list to store the position of each particle at each time step
positions = []
for i in range(len(particles)):
    positions.append([])




# Load the image
background_image = pygame.image.load("bg2.png")

# Scale the image to fit the screen
background_image = pygame.transform.scale(background_image, WINDOW_SIZE)



# Main loop to update the screen
running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        if event.type == pygame.KEYDOWN and event.key == pygame.K_SPACE:
            positions = []
            for i in range(len(particles)):
                positions.append([])
                
        elif event.type == pygame.MOUSEMOTION:
            # Update the black hole position based on the mouse position
            black_hole_x = event.pos[0]
            black_hole_y = event.pos[1]
    pygame.draw.circle(screen, (255,234,180), (black_hole_x, black_hole_y), 20) 
        
            
    
    # Clear the screen
    screen.fill((0, 0, 0))
    screen.blit(background_image, (0, 0))
    
       
    pygame.draw.circle(screen, (255,234,180), (black_hole_x, black_hole_y), black_hole_radius)
    # Draw both black holes
    for bh in black_holes:
        pygame.draw.circle(screen, (255,234,180), (int(bh['x']), int(bh['y'])), bh['radius'])
    


    # Draw the particles representing the stars
    for i, particle_i in enumerate(particles):
        particle_color = colors[i]
        pygame.draw.circle(screen, particle_color, (int(particle_i[0]), int(particle_i[1])), int(particle_i[5]))
        # Calculate the acceleration of particle i due to other particles
        ax = 0
        ay = 0
        for j, particle_j in enumerate(particles):
            if i != j:
                dx = particle_j[0] - particle_i[0]
                dy = particle_j[1] - particle_i[1]
                r = math.sqrt(dx**2 + dy**2)
                #inertial mass
                m_i= particle_i[4]
                a = G * m_i / r**2
                m_i= particle_i[4]* (1 - ((2 * c**2) / (abs(a) * Theta)))
                ax += ((2 * G * m_i * c**2) / Theta)**1/4
                ay += ((2 * G * m_i * c**2) / Theta)**1/4
        
        # Add the effect of the black holes on particle i
        for bh in black_holes:
            dx = bh['x'] - particle_i[0]
            dy = bh['y'] - particle_i[1]
            r = math.sqrt(dx**2 + dy**2)
            a = G * black_hole_mass / r**2
            ax += a * dx / r
            ay += a * dy / r


        # Update the velocity of particle i based on the acceleration
        particle_i[2] += ax / scalefactor
        particle_i[3] += ay / scalefactor

        # Update the position of particle i based on the velocity
        particle_i[0] += particle_i[2] / scalefactor
        particle_i[1] += particle_i[3] / scalefactor
        
        # Add the current position to the list for this particle
        positions[i].append((int(particle_i[0]), int(particle_i[1])))

        # Draw the particle's trajectory
        dash_length = 1
        gap_length = 1
        for j in range(1, len(positions[i])):
            if j % (dash_length + gap_length) < dash_length:
                pygame.draw.aaline(screen, (particle_color), positions[i][j-1], positions[i][j])
        
            
            
    # If the particle has collided with the black hole, remove it and its trajectory

        
    # Add the current position to the list for this particle
        particle_trajectory = []
        particle_trajectory.append((int(particle_i[0]), int(particle_i[1])))
        for i in range(len(particle_trajectory)):
            if i > 0:
                pygame.draw.line(screen, (particle_color[i]), particle_trajectory[i - 1], particle_trajectory[i], 1)
                pygame.draw.circle(screen, particle_color, (int(particle_i[0]), int(particle_i[1])), int(particle_i[5]))

        # Calculate the acceleration of particle i due to the black hole
        dx = black_hole_x - particle_i[0]
        dy = black_hole_y - particle_i[1]
        r = math.sqrt(dx**2 + dy**2)
        a = G * black_hole_mass / r**2
        black_hole_mass= black_hole_mass* (1 - ((2 * c**2) / (abs(a) * Theta)))
        ax += a * dx / r
        ay += a * dy / r

        # Update the velocity of particle i based on the acceleration
        particle_i[2] += ax + (((2 * G * black_hole_mass * c**2) / Theta)**1/4) / 50
        particle_i[3] += ay + (((2 * G * black_hole_mass * c**2) / Theta)**1/4) / 50

        # Update the position of particle i based on the velocity
        particle_i[0] += particle_i[2] / scalefactor
        particle_i[1] += particle_i[3] / scalefactor
        
        # Check if particle is outside the window
        if particle_i[0] < -30 or particle_i[0] > WINDOW_SIZE[0]+30:
            particle_i[2] = - 2
        if particle_i[1] < -30 or particle_i[1] > WINDOW_SIZE[1]+30:
            particle_i[3] =  - 2
        
    

            
        # Check if particle is inside the black hole

        # Update black hole position

    
    # choose a radius for the black hole
    #pygame.draw.circle(screen, (5, 5, 5), (int(black_hole_x), int(black_hole_y)), int(black_hole_radius), 0)
    #pygame.draw.circle(screen, (255, 255, 255), (int(black_hole_x), int(black_hole_y)), int(black_hole_radius), 2)       

            
        


    # Update the screen
    pygame.display.flip()

# Quit Pygame
pygame.quit()

