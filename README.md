Note:
This project is still under-developing

# Material import
First we have accese the data of refractive index vs. lambda 
```python
Si2_file = pd.read_csv('./SiO2.csv')
SiO2_w = SiO2_file['nm'].values
SiO2_n = SiO2_file['n'].values
SiO2_k = SiO2_file['k'].values
```
The material data was stored in 'SiO2.csv' and each data was separated by column
Then registe the materal through method Material.Material()
```python
SiO2 = ml.Material(SiO2_w, SiO2_n, SiO2_k, SiO2_w)
```
The material can be re-acquested by defineding the range of wavelength 'wl'
```python
wl = np.linspace(400, 700, 301)
SiO2.nvalues(wl)
SiO2.kvalues(wl)
```

# Optical spectrum simulation
we add 2 new material 'ambient' and 'substrate' through the method in Material.Non_Dispersion()
```python
void = ml.Non_Dispersion(1)
glass = ml.Non_Dispersion(1.52)
```
To obtaion the optical spectrum, using class thinfilm.Design to build thinfilm model.
First row is material, second row is thickness 
```python
SiO2_thinfilm = tm.Design(
  [void, SiO2, glass],
  [None, 100, None]
)
```
```python
wl = np.linspace(400,700,301)
R = SiO2_thinfilm.reflectance(wl, 0)
print(R)
```


# Index matching optimization

