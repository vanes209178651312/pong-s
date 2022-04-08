# Import the pygame library and initialise the game engine
import pygame
pygame.init()

# Define some colors
WHITE= (255,255,255)
GREEN = (124,252,0)
MAGENTA=(191,62,255)
# Open a new window,caption it "pong"
size = (700, 500)
screen =pygame.display.set_mode ((700, 500))
pygame.display.set_caption("Pong")

#here's the variable that runs our game loop
doExit=False

#The clock will be used to control how fast the screen updates
Clock= pygame.time.Clock()

#variables to hold paddle position
#these go above game Loop
p1x = 20
p1y = 200

p2x=630
p2y=200
p1Score=0
p2Score=0
#ball variables
bx = 350 #xposition
by = 250 #yposition
bVx = 5 #x velocity (horizontal speed)
bVy = 5 #y velocity (vertical speed)

while not doExit:#game loop ------------------------------------------------------------
    Clock.tick(60)
    for event in pygame.event.get():#check if user did something
        if event.type== pygame.QUIT:#check if user clicked close
            doexit= True #flag that we are done so we exit game loop
            
            #game logic will go here----------------------------------------
            
                #game logic-----------------------------
    keys = pygame.key.get_pressed()
    if keys[pygame.K_w]:
        p1y -= 5
    if keys[pygame.K_s]:
        p1y += 5
    if keys[pygame.K_UP]: 
        p2y -= 5
    if keys[pygame.K_DOWN]:
        p2y +=5
    

      # reflect ball off side walls of screen
    if bx <0 or bx +40 >700: #sides
        bVx *=-1
    if by <0 or by + 40 > 500: #top and bottom
        bVy*=-1
        
    if bx <0: #have we hit the back wall
        p1Score +=1
   #reflect ball of side walls of screen,change score
    if bx+40 >700:
        p2Score +=1 #python doesn't do ++ because its dumb 

        
            
        
    #ball-paddle reflection
        #left paddle
    if bx < p1x + 20 and by + 20 > p1y and by < p1y + 100:
        bVx *= -1
        #right paddle
    if bx+30 < p2x and by + 30 > p2y and by < p2y + 100:
        bVx *= 1

    #ball movements
    bx += bVx
    by += bVy
    #print("bvx is ", bVx)
    #print("x is ", bx)
                
    #render (draw)
    screen.fill((238,174,238)) #wipe screen black
            
    #draw a line down the middle
    pygame.draw.line(screen,(124,252,0),[349,0],[349,500],5)
    #draw a rectangle
    pygame.draw.rect(screen, (3, 3, 3), (p1x, p1y, 20, 100), 3)
    #draw a rectangle
    pygame.draw.rect(screen, (3, 3, 3), (p2x, p2y, 20, 100), 3)
    #draw a ellipse
    pygame.draw.ellipse(screen, (0, 238, 238), (bx, by, 30, 30))
    #display scores
    font = pygame.font.Font(None,74)#USE DEFAULT FONT
    text = font.render(str(p1Score),1,(255,255,255))
    screen.blit(text,(250,10))
    text=font.render(str(p2Score),1,(255,255,255))
    screen.blit(text,(420,10))
    #update the screen
    pygame.display.flip()
            
            






            
#END GAME LOOP------------------------------------------------------------
            
pygame.quit()#when game is done close down pygame
