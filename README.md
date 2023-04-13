# countriesAPI
const express = require('express')
const cors = require('cors')

const logger = require("./logger");
const countries = require('./countries.json')
const { capitalise } = require('./helpers')

const app = express()

app.use(cors())
app.use(express.json())
app.use(logger)

app.get('/', (req, res) => {
  res.send("Welcome the Countries API")
})

app.get('/countries', (req, res) => {
  res.send(countries)
})

// Mock data for countries, I think this can go in .json
const countries = [
  { name: 'United States', code: 'US', capital: 'Washington, D.C.' },
  { name: 'Canada', code: 'CA', capital: 'Ottawa' },
  { name: 'Mexico', code: 'MX', capital: 'Mexico City' },
  // ...and so on
];
// I tried to define a route for getting all countries
app.get('/countries', (req, res) => {
  res.json(countries);
});
// I tried to define a route for getting a specific country by code
app.get('/countries/:code', (req, res) => {
  const country = countries.find(c => c.code === req.params.code);
  if (country) {
    res.json(country);
  } else {
    res.status(404).json({ error: 'Country not found' });
  }
});
// This will start the server?
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server listening on port ${PORT}`);
});
