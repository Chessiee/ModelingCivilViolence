# ModelingCivilViolence

This project models the rebellion of a civilian population against a central authority, with a focus on police brutality. It extends Joshua Epstein's civil violence model (2002), built upon Uri Wilensky's NetLogo implementation (2004). The population wanders randomly. If their grievance is high enough and perceived risk is low enough, they rebel. Police officers ("cops") suppress rebellion by arresting agents. Our extension introduces three key innovations: (1) violent cops who can arbitrarily arrest quiet civilians, (2) dynamic government legitimacy that responds to police behavior, and (3) a trauma effect where civilians remember brutality.

## HOW IT WORKS

Civilian Agents:
Grievance is calculated as: G = H × (1 - L) × (1 + U)

H = Perceived hardship 
L = Government legitimacy 
U = Trauma from police brutality


Each agent estimates their arrest probability based on nearby cops and active agents:
P = 1 - exp(-k × C/A), 

where C/A is the cop-to-active ratio within vision.

Activation Rule: If G - (Risk Aversion × P) > T, the agent rebels (turns red).
Otherwise, they stay quiet (green shades show grievance level).

Cop Agents:
Two types of cops:

Ordinary cops (cyan triangles): Only arrest active agents
Violent cops (orange triangles): Can arbitrarily arrest quiet civilians with individual probabilities (0.1-0.7)

Cop Rule: Cops arrest active agents first (fair arrest). If no active agents are nearby and the cop is violent, they may arbitrarily arrest a quiet civilian.

Dynamic Legitimacy:
L(t+1) = L(t) + α × (N_fair - β × N_arbitrary)
Fair arrests slightly increase legitimacy (α = 0.005);
arbitrary arrests decrease it more strongly (β = 2). Bounded between 0 and initial value.

Trauma Effect:
U(t+1) = U(t) + ω × S + γ × N_witnessed - μ
Where S = being arbitrarily arrested (ω = 0.7), N_witnessed = arbitrary arrests witnessed (γ = 0.3), and μ = 0.02 is decay. Bounded 0-1.

Movement and Jail:
Agents move randomly within vision (if enabled). Arrested agents are jailed for 0 to MAX-JAIL-TERM steps, then released with same grievance and trauma.

## HOW TO USE IT
Sliders:

INITIAL-COP-DENSITY: Density of cops
VIOLENT-COP-DENSITY: Percentage of violent cops (0-50%)
INITIAL-AGENT-DENSITY: Density of civilians
VISION: Perception radius for all agents
MAX-GOVERNMENT-LEGITIMACY: Starting legitimacy (becomes dynamic)
MAX-JAIL-TERM: Maximum jail sentence

Controls:

SETUP: Initialize population
GO: Run simulation
MOVEMENT?: Toggle agent movement
TRAUMA?: Enable trauma effect
LEGITIMACY-CHANGE?: Enable dynamic legitimacy
WATCH ONE: Follow agent with highest grievance

Visualization: Choose 2D (circles/triangles) or 3D (people shapes).


## REFERENCES AND CREDITS
This model extends Joshua M. Epstein's civil violence model: "Modeling civil violence: An agent-based computational approach", Proceedings of the National Academy of Sciences, Vol. 99, Suppl. 3, May 14, 2002. Available at https://www.pnas.org/doi/10.1073/pnas.092080199

The implementation builds upon Uri Wilensky's NetLogo Rebellion model (2004): http://ccl.northwestern.edu/netlogo/models/Rebellion

Extension developed by:
Anna Gumenyuk, Joni Baarda, Jiale Li, and Andrei Foitos
University of Groningen, 2025

Original Rebellion model: Copyright 2004 Uri Wilensky.
Extension: Copyright 2025 Anna Gumenyuk, Joni Baarda, Jiale Li, and Andrei Foitos.
