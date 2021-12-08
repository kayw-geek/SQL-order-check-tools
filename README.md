# sql-order-check-tools

A tool used to check the order of columns in SQL table structure.

# Configuration description

```php
// SQL_PATH: Your table structure file path.
define('SQL_PATH', dirname(__DIR__) . DIRECTORY_SEPARATOR . 'mysql' . DIRECTORY_SEPARATOR . 'mysql.sql');
// CACHE_FILE_PATH: Save path and suffix of cache file when configuration `use_cache` is turned on.
define('CACHE_FILE_PATH', getcwd() . '/.' . md5_file(SQL_PATH) . '.sql_report_cache');
const ERROR_CODE        = 0;
const SUCCESS_CODE      = 1;
// Message output when the program detects no abnormality.
const SUCCESS_MESSAGE   = 'Good job!';
// Unspecified remaining columns.
const REMAINING_COLUMNS = '...';
const CONFIG            = [
    'sql_file_path'     => SQL_PATH,

    'similar_adjacent'  => true, // Open similar columns sorting, e.g. user_name, user_age, user.
    'use_cache'         => true,
    'sql_order_rules'   => [
        'id|_id', // If there is an `id` column in the table, it will be ranked first; if there is a field like `xxx_id`, it will be ranked after the `id`.
        // 'type|_type',
        // 'category|_category',
        // 'status',
        REMAINING_COLUMNS, // This is the only place where similar adjacent rules are used
        'created_at',
        'updated_at',
        'deleted_at',
    ],
    'ignore_tables' => [
//         'addresses', // Tables that ignore some special rules.
    ],
];
```
# How to use

Put your MySQL table structure file in the specified folder.
Execute `/src/sql-order-analyse-tools` in the terminal.

# Analysis report

<img width="890" alt="report" src="https://user-images.githubusercontent.com/29700073/145230629-e8c8fb5d-3b29-4d3c-ae78-09761ce2310a.png">

