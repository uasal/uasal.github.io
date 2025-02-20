---
title: "Integrating Sphere Build Process"
categories:
  - design
tags:
  - report
  - blog
author:
  - "Nikoli Cooper, TIMESTEP Apprentice"

---
Commercial Integrating Spheres on the market are high quality, yet expensive. A 6" diameter can cost upwards of $2000. In order to minimize the cost of CMOS characterization, we have devised a procedure to create our own small Integrating Sphere (up to 7" diameter) from scratch.  
**This characterization is distinct from sensor characterization performed at the [UA Imaging Technology Lab](https://itl.arizona.edu/) discussed in other blog posts (e.g. https://uasal.github.io/testing/sensor_reports/)**.

## Design Process  

We designed one 6" and one 7" diameter Integrating Sphere in SolidWorks with a few design criteria:  

- **Surface area covered by ports must be 5% max,** from [Building an Integrating Sphere](http://www.moria.de/tech/integrating-sphere/)
- **Spheres must be 3D printable on a Prusa mk4. (7" max diameter, with flange)**  
- **Outlet port must be able to cover the majority of a Sony IMX455 (1.7" diagonal), and the inlet port must be set up for an optical fiber.**  
- **A baffle must block light from directly exiting from the inlet port.**
<img src="/assets/blog_images/2025-02-15-Integrating-Sphere-build-process-Two_Spheres_with_Fiber.jpg" alt="6 inch and 7 inch diameter Integrating Spheres" width="800"/>

## Fabrication  

1. The two Integrating Spheres were 3D printed on a **Prusa mk4** in PLA. They both have a **2.5" diameter outlet port**, and a **1" diameter inlet port** for use with **[Edmund Optic's 1" SMA adapter](https://www.edmundoptics.com/p/1-sma-adapter-for-4-6-integrating-sphere/32111/)** for optical fiber attachment. Each sphere was printed in two halves and connected via a flange with **8 M6 bolts**.  
2. Following printing, the Spheres were **rigorously sanded with 60 and 80 grit sandpaper** to remove imperfections and texture from the 3D printing process. Any small holes in the inside surface were coated with **Elmer's glue** to prevent paint leakage.  
3. **2 coats of aluminum silver paint** were applied first to make the spheres light-tight and to reflect light above **900 nm**, where the white wall's reflectivity starts to drop off. **Both spheres used a total of 30 ml of silver paint**.  
4. 6 coats of **[Avian B white wall with Barrium Sulfate](https://www.edmundoptics.com/p/250ml-pre-mix-white-reflectance-coating/26992/)** were used as the main high-reflectivity coating. Paint was applied in thin layers and diluted with water (around 50%) for airbrush application. **Coating both spheres used around 1/2 - 2/3 of a 250 ml bottle of Avian B**.  

## Testing  

The main ways to evaluate an Integrating Sphere are by its **sphere multiplier** and its **reflectance**. The calculation methods for these numbers are highlighted in **[this paper](http://www.moria.de/tech/integrating-sphere/)**.  

**Reflectance** is calculated from the sphere multiplier and geometric conditions of the sphere itself. The sphere multiplier is given by:  

Mₛ = (output flux / input flux) × (sphere surface / input port surface) 

And reflectance is given by:

Rₛ =  𝟷 / ( (𝟷 / Mₛ) + 𝟷 - port fraction )

The only unknown value here is **output flux**.  

### 1. Calculating Output Flux  

The output flux is measured using a **PixeLINK PL-D753MU-BL CMOS sensor**.  

- The optical fiber is pointed at the sensor from an arbitrary distance. **Broadband (400 - 2200 nm) light** was used.  
- The sensor captures an image at **3 ms exposure**, yielding an image within its dynamic range.  
- Astropy is used to **calculate the average signal** from the image.  
- The fraction of the surface of the light cone at the sensor plane that the sensor covers is taken as **k**.  
- Then, **input flux × k = i**, where **i** is the flux required to illuminate the sensor to the average signal measured.  
- A second image is taken **through the integrating sphere** at the same exposure time.  
- The ratio between the average signal with and without the integrating sphere is **r**.  
- The fraction of the output port covered by the sensor is **f**.  
- Error calculated as Standard Deviation from 10 separate output flux measurements per sphere.
Thus, the output flux is calculated as:  

**(1 / f) × r × i = output flux**

From here, we can directly compute the **sphere multiplier** and **reflectance**.  

### 2. Results  

#### 6" Sphere:  
- **Sphere multiplier:** 7.06  
- **Reflectance:** 91.6%  
- **Standard Deviation in sphere multiplier:** 0.134 
#### 7" Sphere:  
- **Sphere multiplier:** 8.07 
- **Reflectance:** 92.0%
- **Standard Deviation in sphere multiplier:** 0.145
## Total Cost for a 6" and a 7" Integrating Sphere:
<table>
    <thead>
        <tr>
            <th>Item</th>
            <th>Cost ($)</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Avian B Paint</td>
            <td>280</td>
        </tr>
        <tr>
            <td>PLA Filament</td>
            <td>25</td>
        </tr>
        <tr>
            <td>Silver Paint</td>
            <td>20</td>
        </tr>
        <tr>
            <td>Airbrush</td>
            <td>20</td>
        </tr>
        <tr>
            <td>SMA Adapter</td>
            <td>285</td>
        </tr>
        <tr>
            <td>Hardware Set</td>
            <td>10</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td><strong>Total + tax</strong></td>
            <td><strong>704</strong></td>
        </tr>
    </tfoot>
</table>

### STL previews for Integrating Spheres:

- [6" Sphere](../assets/blog_images/2025-02-15-Integrating-Sphere-build-process-6_inch_Integrating_Sphere.STL)
- [7" Sphere](../assets/blog_images/2025-02-15-Integrating-Sphere-build-process-7_inch_Integrating_Sphere.STL)
