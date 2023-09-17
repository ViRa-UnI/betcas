```javascript
// database-design-mongodb.js

const mongoose = require('mongoose');

// Schema Design

// User Schema
const userSchema = new mongoose.Schema({
  username: {
    type: String,
    required: true,
    unique: true
  },
  email: {
    type: String,
    required: true,
    unique: true
  },
  password: {
    type: String,
    required: true
  },
  bets: [{
    type: mongoose.Schema.Types.ObjectId,
    ref: 'Bet'
  }]
});

// Bet Schema
const betSchema = new mongoose.Schema({
  user: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'User'
  },
  sport: {
    type: String,
    required: true
  },
  amount: {
    type: Number,
    required: true
  },
  result: {
    type: String,
    enum: ['win', 'loss', 'pending'],
    default: 'pending'
  }
});

// Indexes & Optimization

// Index on username for faster user lookup
userSchema.index({ username: 1 });

// Index on sport for faster bet lookup
betSchema.index({ sport: 1 });

// Query Analysis

// Enable MongoDB's query profiler
mongoose.set('profile', true);

// Export the models
const User = mongoose.model('User', userSchema);
const Bet = mongoose.model('Bet', betSchema);

module.exports = {
  User,
  Bet
};
```

This code generates the MongoDB schema design and indexes for the Radhe Exchange platform. It includes the User and Bet schemas, with a one-to-many relationship between users and bets. The User schema includes fields for username, email, password, and an array of bets. The Bet schema includes fields for the user, sport, amount, and result of the bet. Indexes are created on the username and sport fields for faster lookup. MongoDB's query profiler is enabled for query analysis. The User and Bet models are exported for use in other parts of the application.