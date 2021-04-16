# Paraboloide-implicita

from OpenGL.GLUT import *

from OpenGL.GLU import *

from OpenGL.GL import *

from math import pi, cos, sin

from matplotlib import *

from mpl_toolkits.mplot3d import Axes3D

import matplotlib.pyplot as plt

import numpy as np

from pylab import *

import math

fig = plt.figure()

ax = fig.add_subplot(111, projection='3d')

X = np.arange(-5, 5, 0.1)

Y = np.arange(-5, 5, 0.1)

X, Y = np.meshgrid(X, Y)

Z = (X**2 + Y**2)

ax.set_zlim(-10, 20)

ax.plot_surface(X, Y, Z,  alpha=0.9, rstride=4, cstride=4, linewidth=0.5, cmap=cm.summer)

plt.show()

n1 = 50 n2 = 40 r = 2

def f(i,j):

theta = ( (pi() * i) / (n1 -1) ) - (pi() / 2)

phi = 2*pi()*j/(n2-1)

x = r * cos(theta) * cos(phi)

y = r * sin(theta)

z = r * cos(theta) * sin(phi)

return x,y,z
a = 0

n1 = 50

n2 = 50

r = 2

desenhar:

    QUAD_STRIP
    
    for i in range(0,n1): # theta
    
            for j in range(0,n2): # phi
            
                    x,y,z = f(i,j)
                    
                    glVertex3f(x,y,z)
                    
                    x,y,z = f(i,j + 1)
                    
                    glVertex3f(x,y,z)
                    
     FIM DOS PONTOS
def mesh():

glPushMatrix()

glRotatef(a,1.0,0.0,0.0)


for i in range(n1):
    
    glBegin(GL_QUAD_STRIP)
    
    for j in range(n2):
        
        glColor3fv(((1.0*i/(n1-1)),0,1 - (1.0*i/(n1-1))))
        
        x, y, z = f(i,j)
        
        glVertex3f(x,y,z)

        glColor3fv(((1.0*(i+1)/(n1-1)),0,1 - (1.0*(i+1)/(n1-1))))
        
        x, y, z = f(i+1, j)
        
        glVertex3f(x,y,z)
        
    glEnd()


glPopMatrix()
def desenha():

global a

glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT)

mesh()

a+=1

glutSwapBuffers()
def timer(i):

glutPostRedisplay()

glutTimerFunc(10,timer,1)

glutInit(sys.argv)

glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGBA | GLUT_DEPTH | GLUT_MULTISAMPLE)

glutInitWindowSize(1024,1024)

glutCreateWindow(" Paraboloide ")

glutDisplayFunc(desenha)

glEnable(GL_MULTISAMPLE)

glEnable(GL_DEPTH_TEST)

glClearColor(0,0,0,1)

gluPerspective(45,800.0/600.0,0.1,100.0)

glTranslatef(0.0,0.0,-10)

glutTimerFunc(10,timer,1)

glutMainLoop()

n1 = 50

n2 = 50

r = 2

def f(x,y):

return x**2-y**2
M, N = 100, 100

x0, y0 = -2, -2

xf, yf = 2, 2

dx, dy = (xf - x0)/M, (yf - y0)/N

a = 0

def f1(i,j):

theta = (math.pi*i/(n1-1))-(math.pi/2)

phi = 2*math.pi*j/(n2-1)

x = r*math.cos(theta)*math.cos(phi)

y = r*math.sin(theta)

z = r*math.cos(theta)*math.sin(phi)

return x,y,z
def mesh():

glPushMatrix()

glRotatef(a,1.0,0.0,0.0)

glBegin(GL_QUAD_STRIP)

for i in range(0,n1): 
    #glColor3fv(((1.0*i/(n1-1)),0,1 - (1.0*i/(n1-1))))
    
    for j in range(0,n2): 
    
        glColor3fv(((1.0*(i+1)/(n1-1)),0,1 - (1.0*(i+1)/(n1-1))))
        
        x,y,z = f1(i,j)
        
        glVertex3f(x,y,z)
        
        x,y,z = f1(i+1,j)
        
        glVertex3f(x,y,z)

glEnd()

glPopMatrix()
def desenha():

global a

glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT)

mesh()

a+=1

glutSwapBuffers()
def timer(i):

glutPostRedisplay()

glutTimerFunc(10,timer,1)
PROGRAMA PRINCIPAL
glutInit(sys.argv)

glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGBA | GLUT_DEPTH | GLUT_MULTISAMPLE)

glutInitWindowSize(600,600)

glutCreateWindow(" Paraboloide ")

glutDisplayFunc(desenha)

glEnable(GL_MULTISAMPLE)

glEnable(GL_DEPTH_TEST)

glClearColor(0,0,0,1)

gluPerspective(45,800.0/600.0,0.1,100.0)

glTranslatef(0.0,0.0,-10)

glutTimerFunc(10,timer,1)

glutMainLoop()
