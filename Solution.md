### This is the solution I have Created related to Public Health vaccination Programs

```
DECLARE
    -- Step 1: Cursor for all citizens
    CURSOR c_citizens IS
        SELECT citizen_id, full_name FROM citizens;

    -- Step 2: VARRAY of available vaccines
    v_vaccines vaccine_varray := vaccine_varray('COVID-19', 'Polio', 'Hepatitis B', 'Flu', 'HPV');

    -- Step 3: Nested table to hold vaccination records in memory
    v_records vaccination_table := vaccination_table();

    -- Step 4: Associative array to track next dose reminders
    TYPE reminder_array IS TABLE OF DATE INDEX BY PLS_INTEGER;
    v_reminders reminder_array;

    v_counter NUMBER := 0;
BEGIN
    -- Step 5: Loop through citizens using cursor
    FOR rec IN c_citizens LOOP
        v_counter := v_counter + 1;

        -- Skip citizen if ID is NULL using GOTO
        IF rec.citizen_id IS NULL THEN
            GOTO skip_citizen;
        END IF;

        -- Simulate vaccination entry
        v_records.EXTEND;
        v_records(v_counter) := vaccination_obj(
            rec.citizen_id,
            v_vaccines(1),  -- Example: COVID-19
            1,
            SYSDATE,
            SYSDATE + 30  -- Next dose in 30 days
        );

        -- Save next dose reminder
        v_reminders(v_counter) := SYSDATE + 30;

        <<skip_citizen>>
        NULL;  -- Label target for GOTO, does nothing
    END LOOP;

    -- Step 6: Insert vaccination data into table
    FOR i IN 1 .. v_records.COUNT LOOP
        INSERT INTO vaccination_records (
            citizen_id, vaccine_name, dose_number, vaccination_date, next_dose_date
        ) VALUES (
            v_records(i).citizen_id,
            v_records(i).vaccine_name,
            v_records(i).dose_number,
            v_records(i).vaccination_date,
            v_records(i).next_dose_date
        );
    END LOOP;

    -- Step 7: Display reminder info
    DBMS_OUTPUT.PUT_LINE('--- Vaccination Follow-up Reminders ---');
    FOR i IN 1 .. v_reminders.COUNT LOOP
        DBMS_OUTPUT.PUT_LINE('Citizen ID: ' || v_records(i).citizen_id ||
                             ' | Next Dose Date: ' || TO_CHAR(v_reminders(i), 'DD-MON-YYYY'));
    END LOOP;

    COMMIT;
END;
```
