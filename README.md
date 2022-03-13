# Gravity-Calculation
* We plotted different charts in this class
* We learned about Gravity and how we can calculate gravity of a planet

## Steps To Scrape data
  * *Now, just like we have 8 planets in our solar system (Mercury, Venus, Earth, Mars,Jupiter, Saturn, Neptune, Uranus), let’s try to find which other solar system has the
maximum number of planets.*
  * *For this, we have a column named as - solar_system_name in our CSV. We will create a dictionary to maintain the count of planets each solar system has!*
  * *Before we do that, we can see that we have index mentioned in the rows as the first element, but the header’s first element is empty:*
  * *We will quickly fix this and then find the solar system with the maximum number of planet **(code given below)**.*
  * *Here, we will see that the solar system KOI 31 has maximum planets (8).Let’s get the list of all the planets in this solar system **(code given below)**.*
  * *Before we plot charts, let’s look at our data closely. We can see that the columns planet_mass and planet_radius have values with reference to Jupiter or Earth. There are also few values “Unknown”. Let’s make our data uniform **(code given below)**.*
  * *Here, we are removing all unknown planets and are converting all the planets mass and radius in reference to Earth for our ease. We are left with 4,251 planets who’s
value we know with reference to Earth with following metrics: **1 Jupiter Mass** = 317.8 Earth Mass,**1 Jupiter Radius** = 11.2 Earth Radius*
  * *Although that is going to be a bit extreme, we can still survive at 10 times the gravity we have at Earth. Let’s list down all the names of the planets that have
Gravity of 100 or less!.This will give us 3,951 planets.*
  * *Let’s see how many are there with Gravity less than 10?1,012 planets!*
 
## Code is given below
### *Code for adding count of solar systems* 
````
headers[0] = “row_num”
solar_system_planet_count = {}
for planet_data in planet_data_rows:
if solar_system_planet_count.get(planet_data[11]):
 solar_system_planet_count[planet_data[11]] += 1
else:
 solar_system_planet_count[planet_data[11]] = 1
 max_solar_system = max(solar_system_planet_count,
key=solar_system_planet_count.get)
print("Solar system {} has maximum planets {} out of all the solar systems
we have discovered so far!".format(max_solar_system,
solar_system_planet_count[max_solar_system]))

````
### *Code to print planet names in this solar system(planet name is KOI):*
````
hd_10180_planets = []
for planet_data in planet_data_rows:
if max_solar_system == planet_data[11]:
 hd_10180_planets.append(planet_data)
print(len(hd_10180_planets))
print(hd_10180_planets)
````
### *Code for removing unknown values and convert all units to SI unit*
````
temp_planet_data_rows = list(planet_data_rows)
for planet_data in temp_planet_data_rows:
 planet_mass = planet_data[3]
if planet_mass.lower() == "unknown":
 planet_data_rows.remove(planet_data)
 continue
else:
 planet_mass_value = planet_mass.split(" ")[0]
 planet_mass_ref = planet_mass.split(" ")[1]
 if planet_mass_ref == "Jupiters":
 planet_mass_value = float(planet_mass_value) * 317.8
 planet_data[3] = planet_mass_value
 planet_radius = planet_data[7]
if planet_radius.lower() == "unknown":
planet_data_rows.remove(planet_data)
 continue
else:
 planet_radius_value = planet_radius.split(" ")[0]
 planet_radius_ref = planet_radius.split(" ")[2]
 if planet_radius_ref == "Jupiter":
 planet_radius_value = float(planet_radius_value) * 11.2
 planet_data[7] = planet_radius_value

````
## Facts :
* *We can plot the same with all the planets, but let’s understand one thing before that:*
  * *Great Scientist Albert Einstein gave us a formula with which we can calculate the gravity of any planet.*
  * *Here, G is a gravitational constant, which means that it will always be the same. The value of G (Gravitational Constant) is 6.674e-11.*
  * *M(earth) is the mass of Earth (or any other planet if we are calculating it for another planet). Mass of Earth = 5.972e+24*
  * *d is the radius of the planet! Radius of Earth = 6371000*
* *Here, we can see an inverse relation between the radius of the planet and the gravity. The more the radius (and bigger the planet), the lesser would be Gravity.* 
* *But then, we also see a direct relation between the mass of the planet and the gravity. The more the mass of the planet, the more will be the gravity.*
* *Fact - Our Earth’s gravity is 9.8 m/s, and we as humans are accustomed to it. In order for us to exist on any other planet, the gravity should be close to what we
have here.*
* *Mars has a gravity of 3.711 m/s and Moon has a gravity of 1.62 m/s.*
* *Fun Fact - Our standing human bodies can withstand a gravitational force 90 times stronger than earth!*
