# Vue Calculator

This project implements a simple calculator with a clean user interface, built with Vue.js.

[url=https://ibb.co/0RN4pHY7][img]https://i.ibb.co/FLvZkR8r/Screenshot-2025-03-22-at-2-19-39-PM.png[/img][/url]

## Features

- Basic arithmetic operations (addition, subtraction, multiplication, division)
- Clear and delete functionality
- Responsive design that works on desktop and mobile devices
- Decimal number support

## Demo

[Live Demo](https://reimagined-invention-pqpgrv4wq45c69xx-5173.app.github.dev/)

## Installation

### Prerequisites
- Node.js (v14.0.0 or higher recommended)
- npm or yarn

### Clone the Repository
```bash
git clone https://github.com/yourusername/vue-calculator.git
cd vue-calculator
```

### Install Dependencies
```bash
npm install
```

## Usage

### Development Server
Run the development server:
```bash
npm run dev
```
This will start the server at `http://localhost:5173` (or another port if 5173 is in use).

### Build Command
Build the project for production:
```bash
npm run build
```
This creates optimized files in the `dist` directory ready for deployment.

### Preview Production Build
To preview the production build locally:
```bash
npm run preview
```

## Project Structure
```
vue-calculator/
├── public/
├── src/
│   ├── components/
│   │   └── Calculator.vue    # Main calculator component
│   ├── App.vue               # Root component
│   └── main.js               # Entry point
├── package.json
└── README.md
```

## How It Works
The calculator uses Vue's reactive system with the following state:
- `currentOperand`: Current number being entered  
- `previousOperand`: Previous number after an operation is selected  
- `operation`: Current operation (`+`, `-`, `×`, `÷`)  

## Technologies Used
- **Vue.js 3** with Composition API  
- **CSS Grid** and Flexbox for layout  
