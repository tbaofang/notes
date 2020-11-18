


-> HandleLaserScanMessage()
-> HandleLaserScan() 
-> HandleRangefinder()  

-> CollatedTrajectoryBuilder::AddSensorData()

-> Collator::AddSensorData()


----

Node::StartTrajectoryWithDefaultTopics()

-> Node::AddTrajectory()

-> MapBuilderBridge::AddTrajectory()
-> MapBuilder::AddTrajectoryBuilder()

-> CollatedTrajectoryBuilder::CollatedTrajectoryBuilder()

-> Collator::AddTrajectory()  
-> CollatedTrajectoryBuilder::HandleCollatedSensorData()

-> Dispatchable::AddToTrajectoryBuilder()

-> GlobalTrajectoryBuilder::AddSensorData()