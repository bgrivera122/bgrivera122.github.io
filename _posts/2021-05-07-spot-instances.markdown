---
hero_image: https://northslopechillers.com/wp-content/uploads/2019/07/Cool-Server-Room.jpg
---

# Spot Instancing

## When to Use Them

Going by the description of the project, spot instancing sounded like an option that ran hand-in-hand with something like a classic ELB, where instances would be launched based on immediate short-term need. However, upon researching it, spot loading has more to do with workflows that have lenient deadlines -- Think processing documents through a Lambda workflow. For example, automating a resumè processing pipeline; The resumè's will eventually get processed despite outages with spot instances and land where they need to be. Processing documents for a daily or weekly workflow is something that can be done in a stateless fashion, making it a strong candidate for correct spot instance utilization.

## So Far So Good

That being said, our project is aservice and running it on a spot instance is in no uncertain terms a bad idea. It can (and will) be demonstrated that our project is on a spot instance, but in reality environment having your main app run the risk of disappearing is something that will only be explored in academia. As of this writing, the EC2 instances have been converted into spot instances. This was done by utilizing the <code>aws_spot_instance_request</code> resource and using it to replace the regular <code>aws_instance</code>. <code>aws_spot_instance_request</code> is able to accept the same properties as <code>aws_instance</code>, like the instance type and availability zone, but also has it's own properites. For example, <code>wait_for_fulfillment</code> is a vital property since without it, other resources that are depending on the app server having an IP address will fail. It would request for the spot instance, and simply walk away.

The next step is overseeing Lambda and seeing at what level it can be integrated into the project. Project 1 demonstration saw Lamba functioning solely through the console because the scope of it's function was very small. The expanded requirements require more planning, especially with how the team wants to use a spot fleet. I am confident that we should have enough work done in time to be able to demonstrate the concepts for our next presentation.