## Source everything to import packages correctly

The correct order to use when so the agent imports the right versions of libraries.

```
export PYTHONPATH=/home/ajax/Downloads/f1tenth_gym/my_env/lib/python3.10/site-packages:/home/ajax/Downloads/f1tenth_ws/build/f1tenth_gym_ros:/home/ajax/Downloads/f1tenth_ws/install/f1tenth_gym_ros/lib/python3.10/site-packages:/opt/ros/humble/lib/python3.10/site-packages:/opt/ros/humble/local/lib/python3.10/dist-packages:/home/ajax/Downloads/f1tenth_gym/gym/
```

### Getting reset information from the agent

`self.obs, self.reward, self.done, _ = self.env.step(np.array([[self.ego_steer, self.ego_requested_speed]]))`

This line in gym_bridge gets information. `reward` and `info` are not returned by the env so we can skip it. We can still use done. Done is also `True` when we complete 2 laps. Need to work on fixing this.

### How to RL ??
- State --> `/scan`
- Action --> `/cmd_vel`
- Rewards --> -1 / -100 based on `/done`

Should we give reward for moving forward ??
- Giving rewards based on odometry data by calculating the forward direction?
- Penalise based on past speed -> E.g. If speed is less than 0.5

## What works for now 
- SAC agent tries to learn from the env

### What needs to be done
- Add reset function for resetting the environment
- Detect if the car collided with the walls and reset
- Change driving to ackerman steering instead of normal steering 