import java.util.Timer;
import java.util.TimerTask;


    
public class ClockTimer {
	
      private int hours, minutes,  seconds,  miliSeconds;
      private long current_time;
      public ClockTimer() {
		// TODO Auto-generated constructor stub
	}
      ClockTimer clock;
      
      ClockTimer(int hours, int minutes, int seconds, int miliSeconds)
      {
    	  clock=new ClockTimer();
    	  clock.hours=hours;
    	  clock.minutes=minutes;
    	  clock.seconds=seconds;
    	  clock.miliSeconds=miliSeconds;
    	  clock.current_time=clock.hours*60*60*1000+clock.minutes*60*1000+clock.seconds*1000+clock.miliSeconds;
      }
      void Start()
      {
    	  Runnable r = new Runnable() {
  			public void run() {
  				Timer t = new Timer();
  				t.schedule(new TimerTask() {
  				    @Override
  				    public void run() {
  				    	
  				       call_back_1 call1=new call_back_1() {
						
						@Override
						public void onSecondsUpdate(ClockTimer remainingTime) {
							// TODO Auto-generated method stub
							if(clock.current_time>=0)
							System.out.println("function called every second | Time left(in milisec) - "+clock.current_time);	
						
						}
					};
					clock.current_time-=1000;
					call1.onSecondsUpdate(clock);
					if(clock.current_time<=0)
					{
						call_back_2 call2=new call_back_2() {
							
							@Override
							public void onTimerEnd() {
								// TODO Auto-generated method stub
								System.out.println("onTimerend() is called as time is over");
								t.cancel();
								
							}
						}; 
						call2.onTimerEnd();
					}
  				    }
  				    
  				}, 0, 1000);
  				
  			}
  		};
   
  		Thread t = new Thread(r);
  		
  		t.start(); 
      }
}
