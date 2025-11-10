# Tracking-and-Managing-Public-Health-Vaccination-Programs - PL/SQL Assignment

Student Name: Cyusa Divince  
Student ID: 27516

## Title: Tracking and Managing Public Health Vaccination Programs

## 🩺Problem Recap

In a vaccination program (such as for COVID-19, Polio, or Flu), organizations face challenges in tracking which citizen received which vaccine and dose, ensuring citizens receive their next dose on time, accurately recording this data in a database, and managing large numbers of citizens efficiently; performing all of these tasks manually is error-prone and time-consuming.

## ✅Solution

Here’s a **point-by-point mapping of how the solution addresses each step in the code**:

1. **Looping through all citizens using a cursor**

   * The `FOR rec IN c_citizens LOOP` iterates over each citizen in the `citizens` table.
   * This ensures that every citizen is processed automatically, eliminating the need for manual entry.

2. **Skipping invalid entries with a GOTO statement**

   * The `IF rec.citizen_id IS NULL THEN GOTO skip_citizen; END IF;` checks for missing or invalid citizen IDs.
   * This prevents errors and maintains data integrity by skipping citizens without valid IDs.

3. **Storing vaccination data in memory using a nested table**

   * The `v_records` nested table temporarily holds vaccination records before insertion.
   * This allows for validation and manipulation of the data in memory, making the process safer and more flexible.

4. **Assigning vaccines and dose schedules**

   * Each citizen is assigned a vaccine (e.g., `v_vaccines(1)` for COVID-19) and a dose number.
   * The `vaccination_date` is set to `SYSDATE`, and the `next_dose_date` is calculated as `SYSDATE + 30`.

5. **Tracking next dose dates using an associative array**

   * The `v_reminders` array stores the next dose date for each citizen.
   * This makes it easy to generate follow-up reminders without querying the database again.

6. **Inserting valid records into the database**

   * The `FOR i IN 1 .. v_records.COUNT LOOP` inserts all valid vaccination records into the `vaccination_records` table.
   * This automates the database update process and ensures accurate record keeping.

7. **Generating follow-up reminders**

   * The final loop `FOR i IN 1 .. v_reminders.COUNT LOOP` prints each citizen’s ID and next dose date.
   * This provides a clear report for scheduling future vaccinations and ensures no citizen is missed.
  
### **Conclusion**

The PL/SQL code I have written can automates the vaccination process by:

1. Collecting citizen data.
2. Assigning vaccines and dose schedules.
3. Storing vaccination records in memory.
4. Inserting records into the database.
5. Providing follow-up reminders.
6. Handling exceptions (like missing citizen IDs) safely with `GOTO`.

**In short:** it **ensures accurate, efficient, and automated management of vaccination records and follow-ups**.


