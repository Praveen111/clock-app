import React, { Component } from 'react';
import './App.css';

class App extends Component {

  constructor(props) {
    super(props);
  
    this.state = {
      curTime : '',
      timerCounter : 0,
      timeBegin : '',
    }
  }


  startClock = () => {
   
    setTimeout(() => {
      var today = new Date();

      this.setState({curTime : today.toLocaleTimeString()})
      
      }, 500);

}

updateCounter (event) {

this.setState({timerCounter: event.target.value});
console.log(this.state.timerCounter);
}
  


timer() {

  let time = setInterval(() => {
    if(this.state.timerCounter !== 0) {
      this.setState({timerCounter: this.state.timerCounter - 1});
      console.log(this.state);
    }
   else {
    clearInterval(time);
   }
  }, 1000);
}

stopwatch_start() {

    const start = new Date().getTime();
   this.stopWatchref =  setInterval(() => {
    
      let time,elapsed,clockhours,elapsedhours,elapsedminutes,clockseconds,clockminutes,elapsedseconds
  
  
      time = new Date().getTime() - start;
    elapsed = Math.floor(time / 1000);
       if(Math.round(elapsed) === elapsed){
           elapsed += '.0';
       }
    elapsedhours = Math.floor(elapsed / 3600);
    elapsedminutes = Math.floor(elapsed / 60);
    elapsedseconds = elapsed - elapsedminutes * 60;
       if(elapsedseconds < 10){
           clockseconds = "0" + elapsedseconds;
       } else {
            clockseconds = elapsedseconds;
       }
       if(elapsedminutes < 10){
            clockminutes = "0" + elapsedminutes;
       } else {
            clockminutes = elapsedminutes;
       }
       if(elapsedhours < 10){
            clockhours = "0" + elapsedhours;
       } else {
           clockhours = elapsedhours;
       }
   let elapsedtime = clockhours + ":" + clockminutes + ":" + clockseconds;
 
   this.setState({timeBegin: elapsedtime});
  
    }, 10);
}

stopwatch_stop() {
  clearInterval(this.stopWatchref);
}



  render() {
    return (
      <div className="App" onLoad={this.startClock()}>
        <header className="App-header">
      
          <h1 className="App-title">Welcome to Clock App</h1>
        </header>

       <div id="clock-app">
       <br />
       <div id="current">

     <span><b>Current Time : </b> <h1> {this.state.curTime}</h1></span>
       </div>
      <hr />
          <div id="timer">
            <h2>Timer App</h2>
            <label>Enter time (in seconds)</label> <input type="number" onChange={this.updateCounter.bind(this)}/>
           <button onClick={this.timer.bind(this)}>CountDown</button>
         

        <h3>CountDown : {this.state.timerCounter}</h3>

        
          </div>

          <hr />

          <div id="stopwatch">
              <h4>Stop watch</h4>
              <button onClick={this.stopwatch_start.bind(this)}>Start</button>
              <button onClick={this.stopwatch_stop.bind(this)}>Stop</button>
      
              
              <h2>{this.state.timeBegin}</h2>
          </div>
       </div>
      </div>
    );
  }


}

export default App;
