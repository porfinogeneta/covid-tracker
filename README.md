# covid-tracker

## Description
This app was made with https://covid19api.com/ API. The project is meant to be a small Vuejs exercise. It uses framework concepts such as: props passing, signal emission, using external API and style binding. 

## Website link
You can visit the website at given link https://porfinogeneta.github.io/covid-tracker/

## Pie chart
I created Pie Chart using style binding and conic-gradient, background CSS property.
### Please take into accoint that pie chart is NOT mathematically correct!
That's because it takes summary of total confirmed, total deaths and total recovered and count percentages from this sum. In reality it should be counted as follows:  total deaths / total confirmed and so on.

## Usage
Project is meant to be an interesting representation of Covid19 pandemics. 


## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
