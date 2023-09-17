import React from 'react';
import { BrowserRouter as Router, Switch, Route } from 'react-router-dom';
import { Provider } from 'react-redux';
import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
import createSagaMiddleware from 'redux-saga';
import { ThemeProvider } from 'styled-components';
import { socket } from './socket'; // assuming you have a socket.io instance

import rootReducer from './reducers';
import { theme } from './theme'; // assuming you have a theme object
import Home from './components/Home';
import Profile from './components/Profile';
import BettingHistory from './components/BettingHistory';
import LiveChat from './components/LiveChat';

const sagaMiddleware = createSagaMiddleware();
const store = createStore(rootReducer, applyMiddleware(thunk, sagaMiddleware));

sagaMiddleware.run(rootSaga); // assuming you have a rootSaga function

const App = () => {
  return (
    <Provider store={store}>
      <ThemeProvider theme={theme}>
        <Router>
          <Switch>
            <Route exact path="/" component={Home} />
            <Route path="/profile" component={Profile} />
            <Route path="/betting-history" component={BettingHistory} />
            <Route path="/live-chat" component={LiveChat} />
          </Switch>
        </Router>
      </ThemeProvider>
    </Provider>
  );
};

export default App;