# Forward-Kinematics-SCARA-V3-Python
Forward Kinematics Code for SCARA V3
## SCARA-V3

# Import Libraries

import numpy as np

# link lengths in mm

a1 = float(input("a1 = "))
a2 = float(input("a2 = "))
a3 = float(input("a3 = "))
a4 = float(input("a4 = "))

# joint variables: is mm if f, is degrees if theta\

d1 = float(input("d1 = ")) #20 mm

T2 = float(input("T2 = ")) #30 deg

T3 = float(input("T3 = ")) #-90 deg

# Convert Rotation angles (deg to rad)

T2 = (T2/180)*np.pi
T3 = (T3/180)*np.pi

# Parametric Table

PT = [[(0.0/180)*np.pi, (0.0/180)*np.pi, 0, a1+d1],
      [(0.0/180)*np.pi+T2, (0.0/180)*np.pi, a2, 0],
      [(0.0/180)*np.pi+T3, (0.0/180)*np.pi, a4, a3]]

# Homegeneous Transformation Matrix Formula

i = 0
H0_1 = [[np.cos(PT[i][0]), -np.sin(PT[i][0])*np.cos(PT[i][1]), np.sin(PT[i][0])*np.sin(PT[i][1]), PT[i][2]*np.cos(PT[i][0])],
        [np.sin(PT[i][0]), np.cos(PT[i][0])*np.cos(PT[i][1]), -np.cos(PT[i][0])*np.sin(PT[i][1]), PT[i][2]*np.sin(PT[i][0])],
        [0, np.sin(PT[i][1]), np.cos(PT[i][1]), PT[i][3]],
        [0, 0, 0, 1]]       

i = 1
H1_2 = [[np.cos(PT[i][0]), -np.sin(PT[i][0])*np.cos(PT[i][1]), np.sin(PT[i][0])*np.sin(PT[i][1]), PT[i][2]*np.cos(PT[i][0])],
        [np.sin(PT[i][0]), np.cos(PT[i][0])*np.cos(PT[i][1]), -np.cos(PT[i][0])*np.sin(PT[i][1]), PT[i][2]*np.sin(PT[i][0])],
        [0, np.sin(PT[i][1]), np.cos(PT[i][1]), PT[i][3]],
        [0, 0, 0, 1]] 

i = 2
H2_3 = [[np.cos(PT[i][0]), -np.sin(PT[i][0])*np.cos(PT[i][1]), np.sin(PT[i][0])*np.sin(PT[i][1]), PT[i][2]*np.cos(PT[i][0])],
        [np.sin(PT[i][0]), np.cos(PT[i][0])*np.cos(PT[i][1]), -np.cos(PT[i][0])*np.sin(PT[i][1]), PT[i][2]*np.sin(PT[i][0])],
        [0, np.sin(PT[i][1]), np.cos(PT[i][1]), PT[i][3]],
        [0, 0, 0, 1]]

#print("H0_1 = ")
#H0_1 = np.array(np.around(H0_1,3))
#print(H0_1)

#print("H1_2 = ")
#H1_2 = np.array(np.around(H1_2,3))
#print(H1_2)

#print("H2_3 = ")
#H2_3 = np.array(np.around(H2_3,3))
#print(H2_3)

# Multiply Matrices

H0_2 = np.dot(H0_1,H1_2)
H0_3 = np.dot(H0_2, H2_3)

print("H0_3 = ")
H0_3 = np.array(np.around(H0_3,3))
print(H0_3)

