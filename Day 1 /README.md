Day 1: Introduction to DevOps

[](https://github.com/MunilakshmiP/100-days-of-devops/tree/main/Day-1#day-1-introduction-to-devops)

## What is DevOps?

[](https://github.com/MunilakshmiP/100-days-of-devops/tree/main/Day-1#what-is-devops)

DevOps bridges the gap between  **development (Dev)**  and  **operations (Ops)**  teams, enabling effective collaboration. This teamwork, combined with automation, helps deliver software faster and with fewer issues.

**Scenario:**  Imagine a team developing a mobile app. In a non-DevOps setup, developers finish coding and pass it to operations, who may face deployment issues because they weren’t involved earlier. With DevOps, both teams work together from the start. Automated testing catches bugs quickly, and deployment tools release updates seamlessly without delays.

----------

## What is DevSecOps?

[](https://github.com/MunilakshmiP/100-days-of-devops/tree/main/Day-1#what-is-devsecops)

DevSecOps incorporates security as a shared responsibility within DevOps, ensuring that security checks are integrated throughout the software development process.

**Scenario:**  Think of a banking app. With DevSecOps, security testing is embedded early, allowing potential risks to be identified before deployment. This proactive approach safeguards against data breaches and vulnerabilities.

----------

## History of DevOps

[](https://github.com/MunilakshmiP/100-days-of-devops/tree/main/Day-1#history-of-devops)

DevOps emerged from the need for better collaboration between development and operations teams. Traditional methods often separated these areas, leading to misunderstandings and delays during application deployments.

**Scenario:**  In the early web service days, if a new feature failed, the dev team would blame the ops team and vice versa. DevOps was introduced to eliminate this blame game, fostering synchronization and improving software delivery times.

----------

## Benefits of DevOps

[](https://github.com/MunilakshmiP/100-days-of-devops/tree/main/Day-1#benefits-of-devops)

-   **Faster Delivery:**  Regular and automated deployments facilitate frequent updates.
    
    -   _Example:_  A social media app rolls out new features weekly without disrupting user experience.
-   **Improved Collaboration:**  Teams work together with shared goals and responsibilities.
    
    -   _Example:_  A developer and an ops engineer resolve issues quickly through shared tools.
-   **Better Quality:**  Automated testing catches bugs early.
    
    -   _Example:_  An e-commerce site tests all code updates automatically to maintain stability.
-   **Reduced Complexity:**  Automating routine tasks minimizes human error.
    
    -   _Example:_  DevOps automates server updates for an online gaming platform, preventing gameplay issues.
-   **Quick Problem Resolution:**  Real-time monitoring enables faster issue detection.
    
    -   _Example:_  A video streaming service quickly addresses buffering issues to enhance user experience.

----------

## Key DevOps Principles

[](https://github.com/MunilakshmiP/100-days-of-devops/tree/main/Day-1#key-devops-principles)

1.  **Collaboration:**  Close teamwork improves performance.
    
    -   _Example:_  Developers and ops share a dashboard to track site performance.
2.  **Automation:**  Routine tasks are automated to minimize errors.
    
    -   _Example:_  A music app automates updates, ensuring timely delivery.
3.  **Continuous Improvement:**  Enhancing processes and workflows constantly.
    
    -   _Example:_  An online shopping platform regularly refines load times based on feedback.
4.  **Customer-Centric Action:**  User needs are prioritized in decision-making.
    
    -   _Example:_  A food delivery app updates features based on customer feedback.
5.  **End-Goal Focus:**  Aligning every task with the broader objective.
    
    -   _Example:_  A project management tool prioritizes features that boost productivity.

----------

## DevOps Lifecycle Stages

[](https://github.com/MunilakshmiP/100-days-of-devops/tree/main/Day-1#devops-lifecycle-stages)

[![Screenshot 2024-10-27 162649](https://private-user-images.githubusercontent.com/110093082/380494616-90253a14-1c53-4971-808f-546868d9ff13.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzAyOTE2NzksIm5iZiI6MTczMDI5MTM3OSwicGF0aCI6Ii8xMTAwOTMwODIvMzgwNDk0NjE2LTkwMjUzYTE0LTFjNTMtNDk3MS04MDhmLTU0Njg2OGQ5ZmYxMy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQxMDMwJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MTAzMFQxMjI5MzlaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1hZGExYjMzMWM5NDFhZjUxYjU3NDU3NTIxZWNmZGQ0MjU3MDViYWRkMzczMjkwYWVjNDlmNWZiYjg1ODAyMWU0JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.7qQb4WpDb__d0lVMFQXMU0YMIya0byTMN-dygk68CdE)](https://private-user-images.githubusercontent.com/110093082/380494616-90253a14-1c53-4971-808f-546868d9ff13.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzAyOTE2NzksIm5iZiI6MTczMDI5MTM3OSwicGF0aCI6Ii8xMTAwOTMwODIvMzgwNDk0NjE2LTkwMjUzYTE0LTFjNTMtNDk3MS04MDhmLTU0Njg2OGQ5ZmYxMy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQxMDMwJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MTAzMFQxMjI5MzlaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1hZGExYjMzMWM5NDFhZjUxYjU3NDU3NTIxZWNmZGQ0MjU3MDViYWRkMzczMjkwYWVjNDlmNWZiYjg1ODAyMWU0JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.7qQb4WpDb__d0lVMFQXMU0YMIya0byTMN-dygk68CdE)

1.  **Plan:**  Set up a roadmap and identify functionalities and deadlines.
2.  **Code:**  Develop features using version control systems.
3.  **Build:**  Package code into a build.
4.  **Test:**  Ensure functionality works as expected through testing.
5.  **Release:**  Move to staging for final checks before going live.
6.  **Deploy:**  Deploy to the live production environment.
7.  **Operate:**  Monitor performance post-deployment.
8.  **Monitor:**  Utilize tools to track user interaction and performance metrics.

----------

## Conclusion

[](https://github.com/MunilakshmiP/100-days-of-devops/tree/main/Day-1#conclusion)

In summary, we explored DevOps and its evolution into DevSecOps, emphasizing the importance of collaboration and security in the software development lifecycle. By bridging the gap between development and operations, teams achieve faster delivery, improved collaboration, and enhanced security. The key principles, including continuous improvement and customer-centric action, demonstrate how organizations can create high-quality products and ensure customer satisfaction. Integrating these practices is essential for success in today's fast-paced digital landscape.
