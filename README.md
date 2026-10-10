# f1-airfoil-aero-model
Python model of lift, drag and L/D for an F1-style front wing, using thin airfoil theory.
import numpy as np
import matplotlib.pyplot as plt
def lift_coefficient(alpha_deg):
    alpha_rad = np.radians(alpha_deg)
    return 2 * np.pi * alpha_rad

print(lift_coefficient(5))
alphas = np.arange(-5, 16, 1)
cl_values = lift_coefficient(alphas)

plt.plot(alphas, cl_values)
plt.xlabel("Angle of attack (degrees)")
plt.ylabel("Lift coefficient, Cl")
plt.title("Cl vs angle of attack")
plt.grid(True)
plt.show()
AR = 4.0
e = 0.8
Cd0 = 0.01

def total_drag(cl):
    cd_induced = cl**2 / (np.pi * e * AR)
    return Cd0 + cd_induced
    alphas_pos = np.arange(0.5, 15.5, 0.5)
cl_pos = lift_coefficient(alphas_pos)
l_over_d = cl_pos / total_drag(cl_pos)

plt.plot(alphas_pos, l_over_d)
plt.xlabel("Angle of attack (degrees)")
plt.ylabel("L/D")
plt.title("L/D vs angle of attack")
plt.grid(True)
plt.show()

best = np.argmax(l_over_d)
print(alphas_pos[best], l_over_d[best])

