# blender-procedural-scattering
Python Script for collision free procedural object scattering using bounding sphere rejection sampling.

<img width="1686" height="958" alt="image" src="https://github.com/user-attachments/assets/155e96a4-1b70-4024-944c-545e5a8278d6" />


## Key Features

* **Collision-Free Generation:** Utilizes **Bounding Sphere Collision Detection** to guarantee zero mesh overlap, regardless of randomized rotations and scaling.
* **Strict Volume Containment:** Dynamically calculates spatial offsets based on individual mesh scales (`candidate_radius`) to ensure no generated object clips through the boundaries of the defined generation box.
* **Failsafe Rejection Sampling:** Employs an attempt-limit loop (`max_attempts_per_cube`) that safely halts generation if the volume becomes too saturated, preventing infinite loops or viewport freezing.
* **Deterministic Results:** Uses a dedicated, seeded random number generator (`random.Random`) so specific layouts can be perfectly reproduced by keeping the same seed.
* **Modular Primitive Support:** The `add_mesh` helper dynamically accepts uniform/non-uniform scales and cleanly handles different primitive types (Cubes, Spheres, Monkeys, Cylinders, etc.).

## LOGIC: Bounding Sphere Collision
Calculating true OBB (Oriented Bounding Box) collisions of randomly rotated meshes is a computationally overload. This script optimizes collision checks using mathematical bounding spheres.

For a uniform cube of scale `s`, the distance from the center to its furthest corner is calculated using the 3D Pythagorean theorem:
`Radius = s * sqrt(3)`
Before spawning, the script checks the Euclidean distance between the candidate center and all previously placed centers. If the distance is less than the sum of their radii, the location is rejected, guaranteeing a clean layout.

## How to Use

1. Open Blender.
2. Navigate to the **Scripting** workspace.
3. Click **New** and paste the code from `procedural_scatter.py`.
4. Adjust the parameters in the `main()` function:
   ```python
   object_type = 'Cube'        # Try 'Monkey', 'Sphere', or 'Cylinder'
   number_of_objects = 100     # Target density
   vol_x, vol_y, vol_z = 70.0, 50.0, 10.0  # Size of the spawn box
   scale_range = (0.5, 2.5)    # Min and Max scale of objects
<img width="2047" height="1057" alt="image" src="https://github.com/user-attachments/assets/7c91ad7b-edba-47cc-928a-40fcc8be0993" />

<img width="1683" height="935" alt="image" src="https://github.com/user-attachments/assets/2574f10f-d85c-48dd-bc96-f6d7a42d2368" />

https://github.com/user-attachments/assets/cfcdd35e-b5d9-484a-a0f6-8342e7026bc0



