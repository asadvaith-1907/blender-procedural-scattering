# blender-procedural-scattering
Procedural Script for collision free procedural object scattering using bounding sphere rejection sampling.

## Key Features

* **Collision-Free Generation:** Utilizes **Bounding Sphere Collision Detection** to guarantee zero mesh overlap, regardless of randomized rotations and scaling.
* **Strict Volume Containment:** Dynamically calculates spatial offsets based on individual mesh scales (`candidate_radius`) to ensure no generated object clips through the boundaries of the defined generation box.
* **Failsafe Rejection Sampling:** Employs an attempt-limit loop (`max_attempts_per_cube`) that safely halts generation if the volume becomes too saturated, preventing infinite loops or viewport freezing.
* **Deterministic Results:** Uses a dedicated, seeded random number generator (`random.Random`) so specific layouts can be perfectly reproduced by keeping the same seed.
* **Modular Primitive Support:** The `add_mesh` helper dynamically accepts uniform/non-uniform scales and cleanly handles different primitive types (Cubes, Spheres, Monkeys, Cylinders, etc.).
