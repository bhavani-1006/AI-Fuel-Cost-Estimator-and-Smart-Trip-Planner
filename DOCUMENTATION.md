# Project Documentation: AI Smart Fuel Cost Estimator & Smart Trip Planner

## 1. Project title
AI Smart Fuel Cost Estimator & Smart Trip Planner (FuelWise AI)

## 2. Abstract
FuelWise AI is a responsive web application that helps users estimate the fuel and cost needed for a journey. The user enters a route name, distance, vehicle mileage, fuel price, and trip type. The application calculates estimated fuel consumption and expense, stores the estimate, and presents charts and practical recommendations. Browser voice capabilities make data entry and result reading more accessible.

## 3. Problem statement
People often estimate travel fuel expenses mentally, which can lead to inaccurate budgets. A simple tool that calculates fuel requirements consistently and keeps a history of journeys can help users plan their travel budgets more clearly.

## 4. Objectives
- Calculate estimated fuel quantity and travel fuel cost.
- Support one-way and round-trip calculations.
- Save and review previous trip estimates.
- Visualise saved costs and distances with charts.
- Provide practical fuel-saving recommendations.
- Support browser-based voice input and spoken results.
- Practise Python, Flask, HTML, CSS, JavaScript, database integration, and API design.

## 5. Scope
### Included in this starter
- Manual route distance input
- Fuel-cost calculation
- SQLite default database and MySQL configuration
- Trip history and delete action
- Cost and distance charts
- Rule-based recommendations
- Browser voice input and text-to-speech
- Responsive dashboard

### Planned enhancements
- Maps/directions API to retrieve route distance
- Live fuel-price source where legally and technically available
- Optional LLM assistant for natural-language trip questions
- User accounts and private trip history
- Export to CSV/PDF
- Unit and integration tests
- Deployment with environment variables and HTTPS

## 6. Technology stack
| Layer | Technology | Purpose |
|---|---|---|
| Front end | HTML | Page structure |
| Styling | CSS | Responsive visual design |
| Browser behaviour | JavaScript | Form submission, voice, charts |
| Charts | Chart.js | Cost and distance visualisation |
| Back end | Python, Flask | Routes, validation, calculations |
| ORM | Flask-SQLAlchemy | Database access |
| Database | SQLite / MySQL | Store trip estimates |
| Voice | Web Speech API | Speech recognition and speech synthesis |

## 7. System workflow
1. User opens the dashboard.
2. User enters trip distance, mileage, fuel price, and fuel type.
3. JavaScript sends the values to the Flask `/api/calculate` endpoint.
4. Flask validates the input.
5. Python calculates total distance, fuel quantity, and estimated cost.
6. The trip is saved to the configured database.
7. The application returns the result and practical tips as JSON.
8. The dashboard updates the estimate; analytics use saved trips.
9. User can view or delete estimates in Trip History.

## 8. Formulae
Let:
- D = one-way distance in kilometres
- M = vehicle mileage in kilometres per litre
- P = fuel price per litre

For a one-way trip:
- Total distance = D
- Fuel required = D / M
- Estimated cost = (D / M) × P

For a round trip:
- Total distance = 2 × D
- Fuel required = (2 × D) / M
- Estimated cost = ((2 × D) / M) × P

Example: D = 240 km, M = 15 km/L, P = ₹105/L.
- Fuel required = 240 / 15 = 16 L
- Estimated cost = 16 × ₹105 = ₹1,680
- Round trip = 480 km, 32 L, ₹3,360

## 9. Database design
Table: `trip`
- `id`: integer primary key
- `start_location`: starting location text
- `destination`: destination text
- `distance_km`: entered one-way distance
- `mileage_kmpl`: entered mileage
- `fuel_price`: entered price per litre
- `fuel_type`: selected fuel label
- `round_trip`: Boolean flag
- `fuel_needed`: calculated fuel amount
- `estimated_cost`: calculated cost
- `created_at`: creation timestamp

## 10. Main routes
| Route | Method | Purpose |
|---|---|---|
| `/` | GET | Dashboard and recent trips |
| `/api/calculate` | POST | Validate, calculate, save, return JSON |
| `/api/analytics` | GET | Return chart data |
| `/history` | GET | Show saved trip estimates |
| `/history/<id>/delete` | POST | Delete one saved estimate |

## 11. AI component
The starter version uses a transparent rule-based recommendation function. It adds suggestions based on the entered mileage and journey distance. This is not a trained machine-learning model or live generative AI integration.

Future AI extension:
- Add an optional LLM API integration for natural-language travel questions.
- Provide only the trip details required to answer.
- Keep API keys in environment variables.
- Treat AI output as suggestions; do not allow it to override calculated totals.
- Show the formula-based result separately from AI-generated advice.

## 12. Voice component
The Speak Details button uses browser speech recognition when supported. It expects three numbers in this order: distance, mileage, fuel price. The user should check the recognised values before calculation. Read My Estimate uses text-to-speech. Browser support and permissions can vary.

## 13. Validation and testing plan
| Test | Input | Expected result |
|---|---|---|
| Standard trip | 240 km, 15 km/L, ₹105/L | 16 L, ₹1,680 |
| Round trip | Same values, round trip enabled | 480 km, 32 L, ₹3,360 |
| Zero distance | 0 km | Validation error |
| Zero mileage | 0 km/L | Validation error |
| Negative price | -5 | Validation error |
| Decimal values | 12.5 km, 10 km/L, ₹100/L | 1.25 L, ₹125 |
| History | Calculate a valid trip | Estimate appears in history |
| Delete | Delete an existing estimate | Estimate no longer appears |
| Analytics | Save multiple estimates | Charts display saved values |
| Voice unsupported | Browser without recognition API | Helpful fallback message |

## 14. Installation and execution
See `README.md` for exact Windows setup commands, virtual-environment creation, dependency installation, application startup, and MySQL configuration.

## 15. Security and limitations
- Change the default secret key before deployment.
- Never commit database passwords or API keys.
- Use HTTPS and production-grade hosting for deployment.
- Add authentication and authorization before storing personal trip data for multiple users.
- Enable CSRF protection for production forms.
- The starter does not retrieve live route distances or fuel prices.
- Actual fuel use varies with traffic, road conditions, load, driving style, and vehicle condition.

## 16. Future enhancements
1. Maps API and route comparison.
2. Real AI travel assistant with optional LLM integration.
3. Separate electric-vehicle energy calculation in kWh.
4. Login, profile, and saved vehicle details.
5. Fuel-price management and source/date display.
6. CSV/PDF report export.
7. Unit tests, error logging, and deployment.
8. Budget alerts and vehicle-to-vehicle cost comparisons.

## 17. Conclusion
FuelWise AI demonstrates how a practical travel budgeting problem can be addressed with Python and Flask. It combines formula-based calculations, persistent trip history, charts, rule-based advice, and browser voice features. It is designed as a learning foundation that can be expanded with real route data and an optional AI API.
