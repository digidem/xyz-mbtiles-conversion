# xyz-mbtiles-conversion

This repo provides a pathway to convert offline XYZ map tiles to mbtiles format (as used by the new Mapeo map server and Terrastories). This works for both raster and vector tiles. 

For now, there are just instructions to follow using `mbutil` below, but in the future we can expand this repo with scripts to automate these steps.

# Requirements:

- Need Python installed (ideally 3, but 2 works too)
- Need npm installed if running the `recursive-rename` script for vector tile handling.

# Manual instructions for converting tiles to mbtiles:

1. Navigate to directory with this template in terminal: `cd path/to/directory`
2. If not already created, create a virtual environment: `python3 -m venv NAME_OF_ENV`
   - `NAME_OF_ENV` can be an arbitrary name (although keeping it short is recommended)
3. Activate the virtual environment: `source ./NAME_OF_ENV/bin/activate`
   - You need to run this whenever working in this project. This ensures dependencies and other project-specific tooling are properly referenced.
4. Install dependencies: `python3 -m pip install -r requirements.txt`
   - The only dependency used here is [`mbutil`](https://github.com/mapbox/mbutil)
5. Use the installed `mb-util` executable to create the mbtiles file: `./env/bin/mb-util DIRECTORY OUTPUT.mbtiles`
   - `DIRECTORY` points to the path containing the tiles directory you wish to convert. It's relative to where the command is run.
   - `OUTPUT` can be any name
   - See `mbutil` documentation for relevant flags related to tile scheme, image format, etc.
6. When you're done, you can deactivate the virtual environment by running: `deactivate`

# Extra step for vector tiles if they are in `.vector.pbf` format

If your vector tiles end in `.vector.pbf`, you need to first run a script to change the suffix to just `.pbf` instead. In the future, we can write a script to recursively rename all of the files in the tile directory. However, one way to do this is to use a node tool called `recursive-rename`.

1. In the terminal, navigate to the directory containing your XYZ tile directory, and install the tool `npm install recursive-rename`.
2. Run the following command: `rename vector.pbf pbf`. This will batch rename all of the individual tile files in each of the subdirectories per zoom level (0, 1, 2, ...).
3. Now you are ready to use `mbtil` to convert the XYZ directory to mbtiles.