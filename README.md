# CombatFixed
Fixing the combat environment from ma-gym for COMP00124 coursework.

## Bugs fixed

#### v0.0.1
No changes from original other than to create new utils file to avoid cloning the entire repo.

#### v0.0.2
Fix _type bug in get_agent_obs.

#### v.0.03
Add a check in the get_agent_obs to check if the agent is dead. Previously the env would print what the agent would see from its square e.g. if another agent walked into its view or onto its square the env would print that. Now it will print all zeros. (Should still check for agents alive in a training loop to avoid filling memory buffer with zeros.)

Also fixed an error where agents would appear randomly disappear (state was all zeros) before reappearing. The issue was caused by two different methods of updating the agents previous position when they move. __update_agent_view was setting _full_obs of agent_prev_pos to empty while __update_agent_pos was setting _full_obs of curr_pos to empty (i.e. set the current position to empty and move the new one). agent_prev_pos was not updated in step (only at reset) so when __update_agent_view is called every agents initial position is set to empty. So when an agent walks into the initial position of another agent they seem to disappear before reapearing when they next move. Fixed this by just commenting out the call to set agent_prev_pos to empty.

## TODO
* Initialisation issue (env gets stuck when trying to initialise (often with 10 agents) and sometimes causes agents to disappear for the whole game).
