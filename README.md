
---

# octomap_tutor

A tutorial demonstrating how to use [OctoMap](https://github.com/OctoMap/octomap). For additional details and context, see the author’s blog: [cnblogs.com/gaoxiang12](https://cnblogs.com/gaoxiang12).

## Dependencies

1. **OpenCV**  
   ```bash
   sudo apt-get update
   sudo apt-get install libopencv-dev
   ```
2. **Boost**  
   ```bash
   sudo apt-get install libboost-all-dev
   ```
3. **PCL**  
   Follow the instructions at [http://pointclouds.org/](http://pointclouds.org/)  
   or install from Ubuntu repositories (if appropriate for your distro):  
   ```bash
   sudo apt-get install libpcl-dev
   ```
4. **OctoMap**  
   - Clone and build from source: <https://github.com/OctoMap/octomap>  
   - Or install from repositories (e.g., `sudo apt-get install liboctomap-dev`)

## Building the Tutorial

1. **Update OctoMap Path**  
   In `cmake_modules/octomap-config.cmake`, replace the absolute paths to match where you installed OctoMap.  
   For example, change:
   ```cmake
   set(OCTOMAP_INCLUDE_DIRS "/home/zuyuan/octomap_ws/src/octomap/octomap/include")
   set(OCTOMAP_LIBRARY_DIRS "/home/zuyuan/octomap_ws/src/octomap/lib")

   set(OCTOMAP_LIBRARIES
     "/home/zuyuan/octomap_ws/src/octomap/lib/liboctomap.so"
     "/home/zuyuan/octomap_ws/src/octomap/lib/liboctomath.so"
   )
   ```
   to the **actual** include and library paths on your system.

2. **Run the Build Script**  
   From the `octomap_tutor` directory:
   ```bash
   bash build.sh
   ```
   This will create a `build/` folder, run CMake, and compile the executables into `bin/`.

## Usage

Below are some example commands (assuming you’re in the `octomap_tutor` directory and the executables are in `bin/`).

```bash
bin/pcd2octomap <input-file> <output-file>
bin/pcd2colorOctomap <input-file> <output-file>
bin/joinmap
```

### Examples

1. **Convert a PCD file to OctoMap**  
   ```bash
   bin/pcd2octomap data/sample.pcd data/sample.bt
   ```
   Converts `sample.pcd` to the OctoMap file `sample.bt`.

2. **Convert a PCD file to a Color OctoMap**  
   ```bash
   bin/pcd2colorOctomap data/sample.pcd data/sample.bt
   ```
   Converts `sample.pcd` to the color OctoMap file `sample.bt`.

3. **Join Multiple Maps**  
   ```bash
   bin/joinmap
   ```
   Joins the maps defined in `data/keyframe.txt`.

## Visualizing with Octovis

If you have built or installed the `octovis` tool from OctoMap, you can visualize `.ot` or `.bt` files. For instance:

- **If you are in** `~/octomap_ws/src/octomap/` (where `octovis` is located):
  ```bash
  ./bin/octovis ../octomap_tutor/data/sample.ot
  ```
- **Or from anywhere**, provide the full path:
  ```bash
  ~/octomap_ws/src/octomap/bin/octovis ~/octomap_ws/src/octomap_tutor/data/sample.ot
  ```

That’s it! You should now be able to build and run the OctoMap tutorial examples. If you run into any issues, make sure you have the correct paths to OctoMap’s libraries and headers, and that all dependencies are installed properly.