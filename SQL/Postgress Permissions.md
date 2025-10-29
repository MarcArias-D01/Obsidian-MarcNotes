#SQL/command/query 
#SQL/PostgreSQL
Dar permisos de lo que quieras en PostgreSQL.

Ejemplo para dani_odoo.

```SQL
DO $$  
DECLARE  
    tbl_name text;  
  seq_name text;

BEGIN  
    FOR tbl_name IN  
        SELECT table_name  
        FROM information_schema.tables  
        WHERE table_name LIKE '%project%'  
    LOOP  
        EXECUTE format('GRANT SELECT, INSERT, UPDATE ON %I TO dani_odoo;', tbl_name);  
  BEGIN  
        -- Construct the sequence name it follows the naming pattern 'tablename_columnname_seq'  
        seq_name := tbl_name || '_id_seq';  
  
        -- Grant USAGE and UPDATE on the sequence  
        EXECUTE format('GRANT USAGE, UPDATE ON SEQUENCE %I TO dani_odoo;', seq_name);  
    EXCEPTION  
        WHEN others THEN  
          RAISE NOTICE 'Failed to grant permissions on sequence % to dani_odoo: %', seq_name, SQLERRM;  
    END;  
    END LOOP;  
END $$;  
END $$;
```