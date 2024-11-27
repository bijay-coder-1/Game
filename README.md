import pygame as py
import random

py.init()

# Defining colors
white = (255, 255, 255)
red = (255, 0, 0)
black = (0, 0, 0)
green = (0, 255, 0)
blue = (0, 0, 255)
e = (0, 200, 0)
n = (255, 255, 0)
d = (100, 0, 0)
i = (150, 0, 0)
# Creating game window
screen_width = 900
screen_height = 600
screen = py.display.set_mode((screen_width, screen_height))

# Game Title
py.display.set_caption("Snake Game")
py.display.update()

# Background
image = py.image.load("snake2.jpg")
def background_floor(image):
    size = py.transform.scale(image, (900, 600))
    screen.blit(size, (0, 0))

clock = py.time.Clock()
font = py.font.SysFont(None, 55)

def text_screen(text, color, x, y):
    screen_text = font.render(text, True, color)
    screen.blit(screen_text, [x,y])


def plot_snake(screen, color, snk_list, snake_size):
    for x,y in snk_list:
        py.draw.rect(screen, color, [x, y, snake_size, snake_size])
        
def home_screen():
    exit_game = False
    while not exit_game:
        screen.fill((blue))
        text_screen("Welcome to Snake Game", white, 200, 35)
        text_screen("Level 1: Very Easy", green, 200, 85)
        text_screen("Level 2: Easy", e, 200, 135)
        text_screen("Level 3: Normal", n, 200, 185)
        text_screen("Level 4: Difficult", d, 200, 235)
        text_screen("Level 5: Insane", i, 200, 285)
        text_screen("Level 6: Impossible", red, 200, 335)
        for event in py.event.get():
            if event.type == py.QUIT:
                exit_game = True 
            
            if event.type == py.KEYDOWN:
                if event.key == py.K_1:
                    gameloop1()
                if event.key == py.K_2:
                    gameloop2()
                if event.key == py.K_3:
                    gameloop3()
                if event.key == py.K_4:
                    gameloop4()
                if event.key == py.K_5:
                    gameloop5()
                if event.key == py.K_6: 
                    gameloop6()
                
                   
        py.display.update()
        clock.tick(60)

# Creating game loop
def gameloop1():
    exit_game = False
    game_over = False
    snake_x = 45
    snake_y = 100
    velocity_x = 0
    velocity_y = 0
    with open("highscore1.txt", "r") as f :
        highscore = f.read()
    food_x = random.randint(20, 880)
    food_y = random.randint(80, 520)
    score = 0
    init_velocity = 1
    snake_size = 10
    fps = 60
    snk_list = []
    snk_length = 1
    while not exit_game:
        if game_over:
            with open("highscore1.txt", "w") as f :
                f.write(str(highscore))
            init_velocity = 0
            text_screen("GAME OVER!!! PRESS ENTER TO CONTINUE", white, 45, 250)
            text_screen("PRESS BACKSPACE TO RETURN TO HOME", white,60, 310)
            for event in py.event.get():
                if event.type == py.QUIT:
                    exit_game = True
                    
                if event.type == py.KEYDOWN:
                    if event.key == py.K_RETURN:
                        gameloop1()   
                    if event.key == py.K_BACKSPACE:
                        home_screen() 
        else: 
            for event in py.event.get():
                if event.type == py.QUIT:
                    exit_game = True

                if event.type == py.KEYDOWN:
                    if velocity_x == 0:
                        if event.key == py.K_RIGHT:
                            velocity_x = init_velocity
                            velocity_y = 0
                        
                    if velocity_x == 0:
                        if event.key == py.K_LEFT:
                            velocity_x = - init_velocity
                            velocity_y = 0
                        
                    if velocity_y == 0:
                        if event.key == py.K_UP:
                            velocity_y = - init_velocity
                            velocity_x = 0
                        
                    if velocity_y == 0:   
                        if event.key == py.K_DOWN:
                            velocity_y = init_velocity
                            velocity_x = 0

            snake_x = snake_x + velocity_x
            snake_y = snake_y + velocity_y

            if abs(snake_x - food_x)<10 and abs(snake_y - food_y)<10:
                score +=1
                food_x = random.randint(20, 880)
                food_y = random.randint(80, 580)
                snk_length +=5
                if score > int(highscore):
                    highscore = score

            background_floor(image)
            # screen.fill(white)
            text_screen("Score: " + str(score), white, 5, 5)
            text_screen("Highscore:" + str(highscore), black, 5, 40)
            py.draw.rect(screen, red, [food_x, food_y, snake_size, snake_size])


            head = []
            head.append(snake_x)
            head.append(snake_y)
            snk_list.append(head)

            if len(snk_list)>snk_length:
                del snk_list[0]
                
            if head in snk_list[:-1]:
                game_over = True
                
            if snake_x<0 or snake_x>screen_width or snake_y<0 or snake_y>screen_height:
                game_over = True
                # print("Game Over")
            # pygame.draw.rect(screen, black, [snake_x, snake_y, snake_size, snake_size])
            plot_snake(screen, black, snk_list, snake_size)
        py.display.update()
        clock.tick(fps)

    py.quit()
    quit()
def gameloop2():
    exit_game = False
    game_over = False
    snake_x = 45
    snake_y = 100
    velocity_x = 0
    velocity_y = 0
    with open("highscore2.txt", "r") as f :
        highscore = f.read()
    food_x = random.randint(20, 880)
    food_y = random.randint(80, 520)
    score = 0
    init_velocity = 2
    snake_size = 10
    fps = 60
    snk_list = []
    snk_length = 1
    while not exit_game:
        if game_over:
            with open("highscore2.txt", "w") as f :
                f.write(str(highscore))
            init_velocity = 0
            text_screen("GAME OVER!!! PRESS ENTER TO CONTINUE", white, 45, 270)
            text_screen("PRESS BACKSPACE TO RETURN TO HOME", white,60, 310)
            for event in py.event.get():
                if event.type == py.QUIT:
                    exit_game = True
                    
                if event.type == py.KEYDOWN:
                    if event.key == py.K_RETURN:
                        gameloop2()
                    if event.key == py.K_BACKSPACE:
                        home_screen()     
        else: 
            for event in py.event.get():
                if event.type == py.QUIT:
                    exit_game = True

                if event.type == py.KEYDOWN:
                    if velocity_x == 0:
                        if event.key == py.K_RIGHT:
                            velocity_x = init_velocity
                            velocity_y = 0
                        
                    if velocity_x == 0:
                        if event.key == py.K_LEFT:
                            velocity_x = - init_velocity
                            velocity_y = 0
                        
                    if velocity_y == 0:
                        if event.key == py.K_UP:
                            velocity_y = - init_velocity
                            velocity_x = 0
                        
                    if velocity_y == 0:   
                        if event.key == py.K_DOWN:
                            velocity_y = init_velocity
                            velocity_x = 0

            snake_x = snake_x + velocity_x
            snake_y = snake_y + velocity_y

            if abs(snake_x - food_x)<10 and abs(snake_y - food_y)<10:
                score +=1
                food_x = random.randint(20, 880)
                food_y = random.randint(80, 580)
                snk_length +=5
                if score > int(highscore):
                    highscore = score

            background_floor(image)
            # screen.fill(white)
            text_screen("Score: " + str(score), white, 5, 5)
            text_screen("Highscore:" + str(highscore), black, 5, 40)
            py.draw.rect(screen, red, [food_x, food_y, snake_size, snake_size])


            head = []
            head.append(snake_x)
            head.append(snake_y)
            snk_list.append(head)

            if len(snk_list)>snk_length:
                del snk_list[0]
                
            if head in snk_list[:-1]:
                game_over = True
                
            if snake_x<0 or snake_x>screen_width or snake_y<0 or snake_y>screen_height:
                game_over = True
                # print("Game Over")
            # pygame.draw.rect(screen, black, [snake_x, snake_y, snake_size, snake_size])
            plot_snake(screen, black, snk_list, snake_size)
        py.display.update()
        clock.tick(fps)

    py.quit()
    quit()
def gameloop3():
    exit_game = False
    game_over = False
    snake_x = 45
    snake_y = 100
    velocity_x = 0
    velocity_y = 0
    with open("highscore3.txt", "r") as f :
        highscore = f.read()
    food_x = random.randint(20, 880)
    food_y = random.randint(80, 520)
    score = 0
    init_velocity = 4
    snake_size = 10
    fps = 60
    snk_list = []
    snk_length = 1
    while not exit_game:
        if game_over:
            with open("highscore3.txt", "w") as f :
                f.write(str(highscore))
            init_velocity = 0
            text_screen("GAME OVER!!! PRESS ENTER TO CONTINUE", white, 45, 270)
            text_screen("PRESS BACKSPACE TO RETURN TO HOME", white,60, 310)
            for event in py.event.get():
                if event.type == py.QUIT:
                    exit_game = True
                    
                if event.type == py.KEYDOWN:
                    if event.key == py.K_RETURN:
                        gameloop3()
                    if event.key == py.K_BACKSPACE:
                        home_screen()     
        else: 
            for event in py.event.get():
                if event.type == py.QUIT:
                    exit_game = True

                if event.type == py.KEYDOWN:
                    if velocity_x == 0:
                        if event.key == py.K_RIGHT:
                            velocity_x = init_velocity
                            velocity_y = 0
                        
                    if velocity_x == 0:
                        if event.key == py.K_LEFT:
                            velocity_x = - init_velocity
                            velocity_y = 0
                        
                    if velocity_y == 0:
                        if event.key == py.K_UP:
                            velocity_y = - init_velocity
                            velocity_x = 0
                        
                    if velocity_y == 0:   
                        if event.key == py.K_DOWN:
                            velocity_y = init_velocity
                            velocity_x = 0

            snake_x = snake_x + velocity_x
            snake_y = snake_y + velocity_y

            if abs(snake_x - food_x)<10 and abs(snake_y - food_y)<10:
                score +=1
                food_x = random.randint(20, 880)
                food_y = random.randint(80, 580)
                snk_length +=5
                if score > int(highscore):
                    highscore = score

            background_floor(image)
            # screen.fill(white)
            text_screen("Score: " + str(score), white, 5, 5)
            text_screen("Highscore:" + str(highscore), black, 5, 40)
            py.draw.rect(screen, red, [food_x, food_y, snake_size, snake_size])


            head = []
            head.append(snake_x)
            head.append(snake_y)
            snk_list.append(head)

            if len(snk_list)>snk_length:
                del snk_list[0]
                
            if head in snk_list[:-1]:
                game_over = True
                
            if snake_x<0 or snake_x>screen_width or snake_y<0 or snake_y>screen_height:
                game_over = True
                # print("Game Over")
            # pygame.draw.rect(screen, black, [snake_x, snake_y, snake_size, snake_size])
            plot_snake(screen, black, snk_list, snake_size)
        py.display.update()
        clock.tick(fps)

    py.quit()
    quit()
def gameloop4():
    exit_game = False
    game_over = False
    snake_x = 45
    snake_y = 100
    velocity_x = 0
    velocity_y = 0
    with open("highscore4.txt", "r") as f :
        highscore = f.read()
    food_x = random.randint(20, 880)
    food_y = random.randint(80, 520)
    score = 0
    init_velocity = 6
    snake_size = 10
    fps = 60
    snk_list = []
    snk_length = 1
    while not exit_game:
        if game_over:
            with open("highscore4.txt", "w") as f :
                f.write(str(highscore))
            init_velocity = 0
            text_screen("GAME OVER!!! PRESS ENTER TO CONTINUE", white, 45, 270)
            text_screen("PRESS BACKSPACE TO RETURN TO HOME", white,60, 310)
            for event in py.event.get():
                if event.type == py.QUIT:
                    exit_game = True
                    
                if event.type == py.KEYDOWN:
                    if event.key == py.K_RETURN:
                        gameloop4()
                    if event.key == py.K_BACKSPACE:
                        home_screen()     
        else: 
            for event in py.event.get():
                if event.type == py.QUIT:
                    exit_game = True

                if event.type == py.KEYDOWN:
                    if velocity_x == 0:
                        if event.key == py.K_RIGHT:
                            velocity_x = init_velocity
                            velocity_y = 0
                        
                    if velocity_x == 0:
                        if event.key == py.K_LEFT:
                            velocity_x = - init_velocity
                            velocity_y = 0
                        
                    if velocity_y == 0:
                        if event.key == py.K_UP:
                            velocity_y = - init_velocity
                            velocity_x = 0
                        
                    if velocity_y == 0:   
                        if event.key == py.K_DOWN:
                            velocity_y = init_velocity
                            velocity_x = 0

            snake_x = snake_x + velocity_x
            snake_y = snake_y + velocity_y

            if abs(snake_x - food_x)<10 and abs(snake_y - food_y)<10:
                score +=1
                food_x = random.randint(20, 880)
                food_y = random.randint(80, 580)
                snk_length +=5
                if score > int(highscore):
                    highscore = score

            background_floor(image)
            # screen.fill(white)
            text_screen("Score: " + str(score), white, 5, 5)
            text_screen("Highscore:" + str(highscore), black, 5, 40)
            py.draw.rect(screen, red, [food_x, food_y, snake_size, snake_size])


            head = []
            head.append(snake_x)
            head.append(snake_y)
            snk_list.append(head)

            if len(snk_list)>snk_length:
                del snk_list[0]
                
            if head in snk_list[:-1]:
                game_over = True
                
            if snake_x<0 or snake_x>screen_width or snake_y<0 or snake_y>screen_height:
                game_over = True
                # print("Game Over")
            # pygame.draw.rect(screen, black, [snake_x, snake_y, snake_size, snake_size])
            plot_snake(screen, black, snk_list, snake_size)
        py.display.update()
        clock.tick(fps)

    py.quit()
    quit()
def gameloop5():
    exit_game = False
    game_over = False
    snake_x = 45
    snake_y = 100
    velocity_x = 0
    velocity_y = 0
    with open("highscore5.txt", "r") as f :
        highscore = f.read()
    food_x = random.randint(20, 880)
    food_y = random.randint(80, 520)
    score = 0
    init_velocity = 10
    snake_size = 10
    fps = 60
    snk_list = []
    snk_length = 1
    while not exit_game:
        if game_over:
            with open("highscore5.txt", "w") as f :
                f.write(str(highscore))
            init_velocity = 0
            text_screen("GAME OVER!!! PRESS ENTER TO CONTINUE", white, 45, 270)
            text_screen("PRESS BACKSPACE TO RETURN TO HOME", white,60, 310)
            for event in py.event.get():
                if event.type == py.QUIT:
                    exit_game = True
                    
                if event.type == py.KEYDOWN:
                    if event.key == py.K_RETURN:
                        gameloop5()
                    if event.key == py.K_BACKSPACE:
                        home_screen()     
        else: 
            for event in py.event.get():
                if event.type == py.QUIT:
                    exit_game = True

                if event.type == py.KEYDOWN:
                    if velocity_x == 0:
                        if event.key == py.K_RIGHT:
                            velocity_x = init_velocity
                            velocity_y = 0
                        
                    if velocity_x == 0:
                        if event.key == py.K_LEFT:
                            velocity_x = - init_velocity
                            velocity_y = 0
                        
                    if velocity_y == 0:
                        if event.key == py.K_UP:
                            velocity_y = - init_velocity
                            velocity_x = 0
                        
                    if velocity_y == 0:   
                        if event.key == py.K_DOWN:
                            velocity_y = init_velocity
                            velocity_x = 0

            snake_x = snake_x + velocity_x
            snake_y = snake_y + velocity_y

            if abs(snake_x - food_x)<10 and abs(snake_y - food_y)<10:
                score +=1
                food_x = random.randint(20, 880)
                food_y = random.randint(80, 580)
                snk_length +=5
                if score > int(highscore):
                    highscore = score

            background_floor(image)
            # screen.fill(white)
            text_screen("Score: " + str(score), white, 5, 5)
            text_screen("Highscore:" + str(highscore), black, 5, 40)
            py.draw.rect(screen, red, [food_x, food_y, snake_size, snake_size])


            head = []
            head.append(snake_x)
            head.append(snake_y)
            snk_list.append(head)

            if len(snk_list)>snk_length:
                del snk_list[0]
                
            if head in snk_list[:-1]:
                game_over = True
                
            if snake_x<0 or snake_x>screen_width or snake_y<0 or snake_y>screen_height:
                game_over = True
                # print("Game Over")
            # pygame.draw.rect(screen, black, [snake_x, snake_y, snake_size, snake_size])
            plot_snake(screen, black, snk_list, snake_size)
        py.display.update()
        clock.tick(fps)

    py.quit()
    quit()
def gameloop6():
    exit_game = False
    game_over = False
    snake_x = 45
    snake_y = 100
    velocity_x = 0
    velocity_y = 0
    with open("highscore6.txt", "r") as f :
        highscore = f.read()
    food_x = random.randint(20, 880)
    food_y = random.randint(80, 580)
    score = 0
    init_velocity = 15
    snake_size = 10
    fps = 60
    snk_list = []
    snk_length = 1
    while not exit_game:
        if game_over:
            with open("highscore6.txt", "w") as f :
                f.write(str(highscore))
            init_velocity = 0
            text_screen("GAME OVER!!! PRESS ENTER TO CONTINUE", white, 45, 270)
            text_screen("PRESS BACKSPACE TO RETURN TO HOME", white,60, 310)
            for event in py.event.get():
                if event.type == py.QUIT:
                    exit_game = True
                    
                if event.type == py.KEYDOWN:
                    if event.key == py.K_RETURN:
                        gameloop6()
                    if event.key == py.K_BACKSPACE:
                        home_screen()     
        else: 
            for event in py.event.get():
                if event.type == py.QUIT:
                    exit_game = True

                if event.type == py.KEYDOWN:
                    if velocity_x == 0:
                        if event.key == py.K_RIGHT:
                            velocity_x = init_velocity
                            velocity_y = 0
                        
                    if velocity_x == 0:
                        if event.key == py.K_LEFT:
                            velocity_x = - init_velocity
                            velocity_y = 0
                        
                    if velocity_y == 0:
                        if event.key == py.K_UP:
                            velocity_y = - init_velocity
                            velocity_x = 0
                        
                    if velocity_y == 0:   
                        if event.key == py.K_DOWN:
                            velocity_y = init_velocity
                            velocity_x = 0

            snake_x = snake_x + velocity_x
            snake_y = snake_y + velocity_y

            if abs(snake_x - food_x)<10 and abs(snake_y - food_y)<10:
                score +=1
                food_x = random.randint(20, 880)
                food_y = random.randint(80, 580)
                snk_length +=5
                if score > int(highscore):
                    highscore = score

            background_floor(image)
            # screen.fill(white)
            text_screen("Score: " + str(score), white, 5, 5)
            text_screen("Highscore:" + str(highscore), black, 5, 40)
            py.draw.rect(screen, red, [food_x, food_y, snake_size, snake_size])


            head = []
            head.append(snake_x)
            head.append(snake_y)
            snk_list.append(head)

            if len(snk_list)>snk_length:
                del snk_list[0]
                
            if head in snk_list[:-1]:
                game_over = True
                
            if snake_x<0 or snake_x>screen_width or snake_y<0 or snake_y>screen_height:
                game_over = True
                # print("Game Over")
            # pygame.draw.rect(screen, black, [snake_x, snake_y, snake_size, snake_size])
            plot_snake(screen, black, snk_list, snake_size)
        py.display.update()
        clock.tick(fps)

    py.quit()
    quit()
home_screen()

 
