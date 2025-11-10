####creation of Citizens Table

```
CREATE TABLE citizens (
    citizen_id      NUMBER PRIMARY KEY,
    full_name       VARCHAR2(100),
    national_id     VARCHAR2(20),
    phone_number    VARCHAR2(20)
);


--- Insertion of Data into citizens Table

INSERT INTO citizens (citizen_id, full_name, national_id, phone_number) VALUES (1, 'Alice Mugenzi', '119998888', '0788888888');
INSERT INTO citizens (citizen_id, full_name, national_id, phone_number) VALUES (2, 'John Kamanzi', '118887777', '0787777777');
INSERT INTO citizens (citizen_id, full_name, national_id, phone_number) VALUES (3, 'Grace Uwimana', '117776666', '0786666666');
```
