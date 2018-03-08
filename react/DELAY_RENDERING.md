## Method1
```javascript
function mapStateToProps(state) {
  if (state.activePlayer.length > 0) {
    return {
      activePlayer: state.activePlayer
    };
  } else {
    return {};
  }
}
```
https://github.com/gaearon/redux-thunk/issues/80#issuecomment-255546009