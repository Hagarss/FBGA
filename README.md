# FPGA-Based Image Steganography Using LSB and Edge Detection Techniques

## Project Overview
This project implements an advanced steganography system on FPGA hardware that combines two innovative approaches for hiding data within images:
1. **Edge Detection Technique** - Hides more data in image edges where changes are less perceptible
2. **Eye Sensitivity Technique** - Adjusts hidden bits per color channel based on human visual sensitivity

The system was developed using Verilog HDL and implemented on a Xilinx FPGA Genesys 2 kit board.

## Key Features
- Dual approach steganography combining edge detection and human vision sensitivity
- FPGA implementation for high-performance image processing
- Adaptive payload capacity (1-6 bits per pixel)
- High-quality stego images with PSNR values up to 60.19 dB
- Complete hardware/software co-design (MATLAB + Verilog)

## Technical Details

### Algorithms Implemented
1. **Edge Detection with Sobel Filter**
   - Uses 3×3 Sobel kernels for horizontal and vertical edge detection
   - Linear shift buffer technique for efficient pixel processing
   - Threshold-based edge identification

2. **Eye Sensitivity-Based Embedding**
   - Channels prioritized by human eye sensitivity: Blue (least sensitive) → Red → Green (most sensitive)
   - Maximum 2 bits per channel (6 bits per pixel total)

### FPGA Implementation
- **Target Board**: Xilinx Genesys 2 with Spartan-3E (XC3S1600E) FPGA
- **Memory**: 44 BRAM blocks for 256×256 cover image
- **Processing**:
  - RGB to grayscale conversion for edge detection
  - Parallel processing of edge detection and encoding paths
  - Controller module for memory address management

### Performance Metrics
| Message Size | 1 bit/pixel | 2 bits/pixel | 3 bits/pixel | 4 bits/pixel | 5 bits/pixel | 6 bits/pixel |
|-------------|------------|-------------|-------------|-------------|-------------|-------------|
| 32×32       | 60.17 dB   | 60.19 dB    | 60.11 dB    | 57.39 dB    | 56.42 dB    | 55.65 dB    |
| 64×64       | 56.12 dB   | 53.10 dB    | 51.34 dB    | 47.36 dB    | 45.13 dB    | 43.94 dB    |

## Repository Structure
```
├── docs/                   # Documentation and paper
├── matlab/                 # MATLAB scripts for image processing
│   ├── image_preprocessing.m
│   ├── psnr_calculation.m
│   └── ...
├── verilog/                # HDL source code
│   ├── sobel_filter.v
│   ├── eye_sensitivity_encoder.v
│   ├── controller.v
│   └── ...
├── constraints/            # FPGA constraint files
├── sim/                    # Simulation files
└── README.md               # This file
```

## Getting Started

### Prerequisites
- Xilinx Vivado (tested with 2019.2)
- MATLAB (for image preprocessing)
- Genesys 2 FPGA board (or compatible)

### Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/Hagersoliman/fpga-steganography.git
   ```

2. Prepare images using MATLAB scripts:
   ```matlab
   % Convert image to .coe format
   image_preprocessing('cover_image.jpg', 256, 256);
   ```

3. Open project in Vivado:
   ```bash
   vivado fpga-steganography.xpr
   ```

## Results
![image](https://github.com/user-attachments/assets/dcf5d178-1f6c-4f5a-9266-60b3de2bc7fb)
![image](https://github.com/user-attachments/assets/dd52462f-c7c9-4456-86a2-9deef4b5c006)


*Comparison of stego images with different embedding rates*
| PSNR    | 1 bit | 2 bits | 3 bits | 4 bits | 5 bits | 6 bits |
|---------|-------|--------|--------|--------|--------|--------|
| 32×32   | 60.17 | 60.19  | 60.11  | 57.39  | 56.42  | 55.65  |
| 64×64   | 56.12 | 53.10  | 51.34  | 47.36  | 45.13  | 43.94  |


The system successfully hides messages up to 64×64 pixels in 256×256 cover images with:
- Perfect message recovery (zero difference matrix)
- High PSNR values (average 50 dB for 64×64 messages)
- Superior performance compared to existing methods


