# shooter
import pygame
import random
W,H = 700,500
fps = pygame.time.Clock()
class npc:
    def __init__(self,x,y,w,h,png):
        self.x = x
        self.y = y
        self.w = w
        self.h = h
        self.png = png
        self.img_new = pygame.transform.scale(pygame.image.load(self.png), (self.w, self.h))
        self.rect = self.img_new.get_rect(center=(self.x, self.y))
a = random.randint(0,W)
sx = random.randint(-2,2)
sy = random.randint(1,2)
player = npc(350,450,80,100,"rocket.png")
asteroid = npc(a,-40,50,50,"asteroid.png")
hard1 = npc(50,50,50,50,"hard.png")
hard2 = npc(75,50,50,50,"hard.png")
hard3 = npc(100,50,50,50,"hard.png")
fon = pygame.transform.scale(pygame.image.load('galaxy.jpg'), (W, H))
screen = pygame.display.set_mode((W,H))
pygame.display.set_caption('shooter')
run = True
move = 2
a =[]
while run:
    while run:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                run = False
        key = pygame.key.get_pressed()
        if key[pygame.K_LEFT] and player.rect.left >= 0:
            player.rect.x -= move
        key = pygame.key.get_pressed()
        if key[pygame.K_RIGHT] and player.rect.right <= W:
            player.rect.x += move
        if key[pygame.K_UP]:
            a.append(npc(player.rect.x + 40,player.rect.top,15,30,"bullet.png"))
        screen.blit(fon,(0,0))
        screen.blit(player.img_new,player.rect)
        screen.blit(hard1.img_new, hard1.rect)
        screen.blit(hard2.img_new, hard2.rect)
        screen.blit(hard3.img_new, hard3.rect)
        for el in a:
            screen.blit(el.img_new,el.rect)
            el.rect.y -= move
        fps.tick(70)
        pygame.display.update()
