<img width="992" height="895" alt="question3 b" src="https://github.com/user-attachments/assets/2939e593-b969-4328-b552-77e316a2da62" />## Questin 3: Suspicious Login Monitoring (Advanced Triggers)
Overview: The goal was to monitor user logins and issue an immediate security alert if any user failed to log in more than two times in the same day.

Implementation:

Tables Created: LOGIN_AUDIT (to track all attempts) and SECURITY_ALERTS (to store policy violations).
Solution: A single AFTER INSERT trigger (trg_CheckSuspiciousLogin) was created on the LOGIN_AUDIT table.
<img width="959" height="504" alt="question3 a" src="https://github.com/user-attachments/assets/15071f46-45a2-4f98-a23a-f54713095e1c" />

Logic: The trigger checked if the inserted record's status was 'FAILED'. If so, it performed a COUNT(*) query on LOGIN_AUDIT for the same user on the current day (TRUNC(SYSTIMESTAMP)).
Alerting: If the count was 
≥
3
, the trigger, operating under PRAGMA AUTONOMOUS_TRANSACTION, inserted a new record into SECURITY_ALERTS and executed an independent COMMIT.
Optional: A second trigger was outlined to demonstrate how to use UTL_MAIL to send an external email notification whenever a record was inserted into SECURITY_ALERTS. 
<img width="992" height="895" alt="question3 b" src="https://github.com/user-attachments/assets/db56fc38-a32a-492e-a706-65fb9eb42aac" />
<img width="975" height="695" alt="question3 b1" src="https://github.com/user-attachments/assets/402b419c-34b4-457b-aa92-b44bc2ffccf3" />

