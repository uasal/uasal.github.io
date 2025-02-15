<table style="border-collapse: collapse; width: 100%; text-align: left;">
  <tr>
    <th style="border: 1px solid black; padding: 8px;">title</th>
    <th style="border: 1px solid black; padding: 8px;">categories</th>
    <th style="border: 1px solid black; padding: 8px;">tags</th>
    <th style="border: 1px solid black; padding: 8px;">author</th>
  </tr>
  <tr>
    <td style="border: 1px solid black; padding: 8px;">Integrating Sphere Build Process</td>
    <td style="border: 1px solid black; padding: 8px;"><span style="border: 1px solid gray; padding: 4px; display: inline-block;">design</span></td>
    <td style="border: 1px solid black; padding: 8px;">
      <span style="border: 1px solid gray; padding: 4px; display: inline-block;">reports</span>
      <span style="border: 1px solid gray; padding: 4px; display: inline-block;">blog</span>
    </td>
    <td style="border: 1px solid black; padding: 8px;"><span style="border: 1px solid gray; padding: 4px; display: inline-block;">Nikoli Cooper</span></td>
  </tr>
</table>

Commercial Integrating Spheres on the market are high quality, yet excessively expensive. It is in excess of $2000 for a 6" diameter Sphere from Edmund Optics. In order to mitigate the cost of our CMOS characterization lab, we have devised a procedure to create our own small Integrating Sphere (up to 7" diameter) from scratch.  

## Design Process  

We designed one 6" and one 7" diameter Integrating Sphere in SolidWorks with a few design criteria:  

- **Surface area covered by ports must be 5% max.**  
- **Spheres must be 3D printable on a Prusa mk4.**  
- **Outlet port must be able to cover the majority of a Sony IMX455, and the inlet port must be set up for an optical fiber.**  
- **A baffle must block light from directly exiting from the inlet port.**  

## Fabrication  

1. The two Integrating Spheres were 3D printed on a **Prusa mk4** in PLA. They both have a **2.5" diameter outlet port**, and a **1" diameter inlet port** for use with **[Edmund Optic's 1" SMA adapter](https://www.edmundoptics.com/p/1-sma-adapter-for-4-6-integrating-sphere/32111/)** for optical fiber attachment. Each sphere was printed in two halves and connected via a flange with **8 M6 bolts**.  
2. Following printing, the Spheres were **rigorously sanded** with **60 and 80 grit sandpaper** to remove imperfections and texture from the 3D printing process. Any small holes in the inside surface were coated with **Elmer's glue** to prevent paint leakage.  
3. **2 coats of aluminum silver paint** were applied first to make the spheres light-tight and to reflect any light above **900 nm**, where the white wall's reflectivity starts to drop off. **Both spheres used a total of 2oz of silver paint**.  
4. 6 coats of **[Edmund Optic's Avian B white wall with Titanium Dioxide](https://www.edmundoptics.com/p/250ml-pre-mix-white-reflectance-coating/26992/)** were used as the main high-reflectivity coating. Paint was applied in thin layers and diluted with **water (around 50%)** for airbrush application. **Coating both spheres used around 1/2 - 2/3 of a bottle of Avian B**.  

## Testing  

The main ways to evaluate an Integrating Sphere are by its **sphere multiplier** and its **reflectivity**. The calculation methods for these numbers are highlighted in **[this paper](http://www.moria.de/tech/integrating-sphere/)**.  

**Reflectivity** is calculated from the sphere multiplier and geometric conditions of the sphere itself. The sphere multiplier is given by:  

Mₛ = (output flux / input flux) × (sphere surface / input port surface) 

The only unknown value here is **output flux**.  

### 1. Calculating Output Flux  

The output flux is measured using a **PixeLINK PL-D753MU-BL CMOS sensor**.  

- The optical fiber is pointed at the sensor from an arbitrary distance.  
- The sensor captures an image at **3 ms exposure**, yielding an image within its dynamic range.  
- **Astropy** is used to calculate the **average signal** from the image.  
- The fraction of the light cone surface at the sensor plane covered by the sensor is taken as **k**.  
- Then, **input flux × k = i**, where i is the flux required to illuminate the sensor to the measured average signal.  
- A second image is taken **through the integrating sphere** at the same exposure time.  
- The ratio between the **average signal with and without the integrating sphere** is **r**.  
- The fraction of the output port covered by the sensor is **f**.  

Thus, the output flux is calculated as:  

**(1 / f) × r × i = output flux**

From here, we can directly compute the **sphere multiplier** and **reflectivity**.  

### 2. Results  

#### 6" Sphere:  
- **Sphere multiplier:** 6.84  
- **Reflectivity:** 91.25%  

#### 7" Sphere:  
- **Sphere multiplier:** (to be determined)  
- **Reflectivity:** (to be determined)  