
# FastNoise Lite

An extremely portable, high-performance noise generation library with a wide selection of noise algorithms. FastNoise Lite avoids platform-specific features, making it flexible and efficient across multiple environments.

[![npm](https://img.shields.io/npm/v/fastnoise-lite?logo=npm)](https://www.npmjs.com/package/fastnoise-lite) [![GitHub](https://img.shields.io/badge/GitHub-black?logo=github)](https://github.com/Auburn/FastNoiseLite)

## Features

- **Multiple Noise Types**: Supports OpenSimplex2, OpenSimplex2S, Cellular, Perlin, ValueCubic, and Value noise algorithms.
- **Fractal Options**: Includes FBm, Ridged, PingPong, and Domain Warp fractal methods.
- **3D Rotation**: Reduces directional artifacts in 3D noise generation.
- **Cellular Noise Customization**: Fine-tune cellular noise with custom distance functions and return types.
- **Domain Warping**: Supports advanced domain warp techniques with various algorithms.

## Installation

To install via npm:

```bash
npm install fastnoise-lite
```

## Basic Usage

Here's a basic example of how to generate 2D noise using FastNoise Lite:

```javascript
import FastNoiseLite from "fastnoise-lite";

function generateNoise(width, height) {
  const noise = new FastNoiseLite();
  noise.SetNoiseType(FastNoiseLite.NoiseType.OpenSimplex2);

  const noiseData = [];
  for (let x = 0; x < width; x++) {
    noiseData[x] = [];
    for (let y = 0; y < height; y++) {
      noiseData[x][y] = noise.GetNoise(x, y);
    }
  }
  return noiseData;
}

const noiseData = generateNoise(126, 126);
```

### Customizing Noise Types

You can easily switch between different noise types using the `SetNoiseType` method:

```javascript
function generateNoise(width, height, type) {
  const noise = new FastNoiseLite();
  noise.SetNoiseType(FastNoiseLite.NoiseType[type]);

  const noiseData = [];
  for (let x = 0; x < width; x++) {
    noiseData[x] = [];
    for (let y = 0; y < height; y++) {
      noiseData[x][y] = noise.GetNoise(x, y);
    }
  }
  return noiseData;
}

const openSimplex2Noise = generateNoise(126, 126, 'OpenSimplex2');
const perlinNoise = generateNoise(126, 126, 'Perlin');
```

## API Reference

### Constructor

```javascript
new FastNoiseLite([seed])
```

- **seed** (optional): Initializes the noise generator with an optional seed for consistent results.

### Methods

#### `SetSeed(seed)`
Sets the seed used for noise generation.

#### `SetFrequency(frequency)`
Sets the frequency (scale) of the noise. Higher frequency creates more detailed noise patterns.

#### `SetNoiseType(noiseType)`
Defines the type of noise algorithm to use. Available noise types are:

- `FastNoiseLite.NoiseType.OpenSimplex2`
- `FastNoiseLite.NoiseType.OpenSimplex2S`
- `FastNoiseLite.NoiseType.Cellular`
- `FastNoiseLite.NoiseType.Perlin`
- `FastNoiseLite.NoiseType.ValueCubic`
- `FastNoiseLite.NoiseType.Value`

#### `SetFractalType(fractalType)`
Sets the method for combining octaves in fractal noise. Available options are:

- `FastNoiseLite.FractalType.FBm`
- `FastNoiseLite.FractalType.Ridged`
- `FastNoiseLite.FractalType.PingPong`
- `FastNoiseLite.FractalType.DomainWarp`

#### `SetFractalOctaves(octaves)`
Defines the number of layers (octaves) for fractal noise. More octaves increase complexity.

#### `SetFractalLacunarity(lacunarity)`
Controls how much detail increases with each octave. A higher lacunarity results in smaller, more detailed features.

#### `SetFractalGain(gain)`
Defines how amplitude decreases with each octave. Lower gain reduces the effect of higher octaves.

#### `SetFractalWeightedStrength(weightedStrength)`
Sets the weighting for the fractal noise's octaves (excluding Domain Warp fractal types).

#### `SetFractalPingPongStrength(pingPongStrength)`
Sets the strength of the Ping Pong fractal effect, which can create unique visual patterns.

#### `SetCellularDistanceFunction(cellularDistanceFunction)`
Defines the distance function used in Cellular noise. Available options are:

- Euclidean
- Manhattan
- Natural

#### `SetCellularReturnType(cellularReturnType)`
Defines what the Cellular noise returns. Examples include cell value, distance to the nearest point, or distance to multiple points.

#### `SetCellularJitter(cellularJitter)`
Sets the maximum displacement of points in Cellular noise.

#### `SetDomainWarpType(domainWarpType)`
Sets the domain warping algorithm for advanced distortion effects.

#### `SetDomainWarpAmp(domainWarpAmp)`
Sets the intensity of domain warping, which controls how much the noise is "warped" from its original position.

### Method Overloading Simulation

Since JavaScript does not natively support method overloading, some FastNoise Lite methods simulate overloading based on the number of arguments. For example:

```javascript
class FastNoiseLite {
    Method() {
        const R2 = (param1, param2) => {
            // Handle 2D noise generation
        }

        const R3 = (param1, param2, param3) => {
            // Handle 3D noise generation
        }

        if (arguments.length === 2) {
            return R2(arguments[0], arguments[1]);
        }

        if (arguments.length === 3) {
            return R3(arguments[0], arguments[1], arguments[2]);
        }
    }
}
```

## Noise Types

FastNoise Lite supports the following noise algorithms:

- **OpenSimplex2**: Fast and versatile noise, great for organic-looking patterns.
- **OpenSimplex2S**: Skewed version of OpenSimplex2.
- **Cellular**: Creates cell-like structures, great for Voronoi diagrams and distance-based effects.
- **Perlin**: Classic gradient noise, useful for smooth transitions and terrain generation.
- **ValueCubic**: A cubic interpolation of value noise, smoother than basic value noise.
- **Value**: Simple value noise, mainly for educational purposes.

## Fractal Types

Fractal types are methods for combining multiple octaves of noise to create more complex patterns. Available fractal types include:

- **FBm**: Fractal Brownian Motion, the most common fractal method, adds multiple octaves of noise.
- **Ridged**: A variation of FBm, with sharper features and inverted ridges.
- **PingPong**: Generates alternating peaks and valleys, creating a unique visual effect.
- **DomainWarp**: Warps the domain of the noise function, distorting the results for interesting patterns.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgements

- Original C++ implementation by Jordan Peck.
- Ported to JavaScript by Patrick U (snowfoxsh).

## Contributing

Contributions are welcome! Please submit a Pull Request or contact us if you would like to contribute.

If you have any questions, feel free to reach out via our [Discord](https://discord.com/) or contact dev_storm on Discord or via email.
