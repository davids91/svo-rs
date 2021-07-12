# svo-rs
Sparse Voxel Octree (SVO) library, entirely `#![no_std]`.

# Usage
```rust
use nalgebra::vector;
use svo_rs::Octree;

// Create an `Octree` with dimensions of 32*32*32, to store `u8` data.
let mut octree = Octree::<u8>::new(NonZeroU32::new(32).unwrap()).unwrap();

// Insert a value of 1 into the `Octree` at position [0, 0, 0].
octree.insert(vector![0, 0, 0], 1);
assert!(matches!(octree.get(vector![0, 0, 0], Some(1))));

// `Octree` simplification used where possible.
// The following will now be condensed to a single leaf node with dimensions of 2*2*2:
octree.insert(vector![0, 0, 1], 1);
octree.insert(vector![0, 1, 0], 1);
octree.insert(vector![0, 1, 1], 1);
octree.insert(vector![1, 0, 0], 1);
octree.insert(vector![1, 0, 1], 1);
octree.insert(vector![1, 1, 0], 1);
octree.insert(vector![1, 1, 1], 1);

// Clear values from the `Octree`.
```
