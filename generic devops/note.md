# generic_devops

## How does a canary deployment work?

<!-- notecardId: 1763281979863 -->

you create a duplicate of the existing infrastructure where you put the new version and you move an increasing percentage of trafic from the old version to the new one

## How does a rolling deployment work?

<!-- notecardId: 1763281979866 -->

you scale down nr of pods in the infra with the old version and scale up nr pods in the new version at the same time

## How does a blue green deployment work?

<!-- notecardId: 1763281979869 -->

you create a duplicate of the existing infrastructure where you put the new version and then switch all trafic at once to it 