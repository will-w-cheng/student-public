---
title: JS Output w/ jquery
toc: True
description: A Tech Talk on outputs using HTML and Javascript. This uses jquery for easy onscreen interaction and filtering.
courses: {'csp': {'week': 2}}
categories: ['C3.0', 'C3.1', 'C4.1']
type: hacks
---

```python
%%html

<head>
    <link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/1.13.4/css/jquery.dataTables.min.css">
    <script type="text/javascript" language="javascript" src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script>var define = null;</script>
    <script type="text/javascript" language="javascript" src="https://cdn.datatables.net/1.13.4/js/jquery.dataTables.min.js"></script>
    
    <style>
        /* Apply styles to the table */
        table {
            width: 100%;
            border-collapse: collapse;
            margin-bottom: 20px;
        }

        th, td {
            padding: 10px;
            text-align: left;
            border-bottom: 1px solid #ddd;
        }

        th {
            background-color: #535136;
            font-weight: bold;
        }

        tbody tr:nth-child(even) {
            background-color: #c0ffee; /* Change this color to your preference */
        }

        /* Add some padding to the description column */
        td:last-child {
            padding-right: 20px;
        }
    </style>
</head>
<head class="hi">
    <link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/1.13.4/css/jquery.dataTables.min.css">
    <script type="text/javascript" language="javascript" src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script>var define = null;</script>
    <script type="text/javascript" language="javascript" src="https://cdn.datatables.net/1.13.4/js/jquery.dataTables.min.js"></script>
</head>


<body>
    <table id="demo" class="table">
        <thead>
            <tr>
                <th>Event</th>
                <th>Date</th>
                <th>Location</th>
                <th>Participants</th>
                <th>Description</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>Attack on Pearl Harbor</td>
                <td>December 7, 1941</td>
                <td>Pearl Harbor, Hawaii</td>
                <td>Imperial Japanese Navy</td>
                <td>Surprise military strike by the Japanese, leading to the United States entry into WW2.</td>
            </tr>
            <tr>
                <td>D-Day (Operation Overlord)</td>
                <td>June 6, 1944</td>
                <td>Normandy, France</td>
                <td>Allied Forces (US, UK, Canada)</td>
                <td>Massive Allied amphibious assault on Nazi-occupied Europe.</td>
            </tr>
            <tr>
                <td>Battle of Stalingrad</td>
                <td>August 23, 1942 - February 2, 1943</td>
                <td>Stalingrad, Soviet Union</td>
                <td>Soviet Red Army vs. Nazi Germany</td>
                <td>One of the deadliest battles in history, resulting in a Soviet victory.</td>
            </tr>
            <tr>
                <td>Hiroshima and Nagasaki Atomic Bombings</td>
                <td>August 6 and 9, 1945</td>
                <td>Hiroshima and Nagasaki, Japan</td>
                <td>United States</td>
                <td>Use of atomic bombs leading to Japanese surrender and the end of WW2.</td>
            </tr>
            <tr>
                <td>Nuremberg Trials</td>
                <td>November 20, 1945 - October 1, 1946</td>
                <td>Nuremberg, Germany</td>
                <td>International Military Tribunal</td>
                <td>Legal proceedings against prominent Nazi leaders for war crimes.</td>
            </tr>
        </tbody>
    </table>


    <script>
        $(document).ready(function () {
            $('#demo').DataTable();
        });
    </script>
</body>




```



<head>
    <link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/1.13.4/css/jquery.dataTables.min.css">
    <script type="text/javascript" language="javascript" src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script>var define = null;</script>
    <script type="text/javascript" language="javascript" src="https://cdn.datatables.net/1.13.4/js/jquery.dataTables.min.js"></script>

    <style>
        /* Apply styles to the table */
        table {
            width: 100%;
            border-collapse: collapse;
            margin-bottom: 20px;
        }

        th, td {
            padding: 10px;
            text-align: left;
            border-bottom: 1px solid #ddd;
        }

        th {
            background-color: #535136;
            font-weight: bold;
        }

        tbody tr:nth-child(even) {
            background-color: #c0ffee; /* Change this color to your preference */
        }

        /* Add some padding to the description column */
        td:last-child {
            padding-right: 20px;
        }
    </style>
</head>
<head class="hi">
    <link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/1.13.4/css/jquery.dataTables.min.css">
    <script type="text/javascript" language="javascript" src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script>var define = null;</script>
    <script type="text/javascript" language="javascript" src="https://cdn.datatables.net/1.13.4/js/jquery.dataTables.min.js"></script>
</head>


<body>
    <table id="demo" class="table">
        <thead>
            <tr>
                <th>Event</th>
                <th>Date</th>
                <th>Location</th>
                <th>Participants</th>
                <th>Description</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>Attack on Pearl Harbor</td>
                <td>December 7, 1941</td>
                <td>Pearl Harbor, Hawaii</td>
                <td>Imperial Japanese Navy</td>
                <td>Surprise military strike by the Japanese, leading to the United States entry into WW2.</td>
            </tr>
            <tr>
                <td>D-Day (Operation Overlord)</td>
                <td>June 6, 1944</td>
                <td>Normandy, France</td>
                <td>Allied Forces (US, UK, Canada)</td>
                <td>Massive Allied amphibious assault on Nazi-occupied Europe.</td>
            </tr>
            <tr>
                <td>Battle of Stalingrad</td>
                <td>August 23, 1942 - February 2, 1943</td>
                <td>Stalingrad, Soviet Union</td>
                <td>Soviet Red Army vs. Nazi Germany</td>
                <td>One of the deadliest battles in history, resulting in a Soviet victory.</td>
            </tr>
            <tr>
                <td>Hiroshima and Nagasaki Atomic Bombings</td>
                <td>August 6 and 9, 1945</td>
                <td>Hiroshima and Nagasaki, Japan</td>
                <td>United States</td>
                <td>Use of atomic bombs leading to Japanese surrender and the end of WW2.</td>
            </tr>
            <tr>
                <td>Nuremberg Trials</td>
                <td>November 20, 1945 - October 1, 1946</td>
                <td>Nuremberg, Germany</td>
                <td>International Military Tribunal</td>
                <td>Legal proceedings against prominent Nazi leaders for war crimes.</td>
            </tr>
        </tbody>
    </table>


    <script>
        $(document).ready(function () {
            $('#demo').DataTable();
        });
    </script>
</body>






### HTML Table with JavaScript jquery
JavaScript is a programming language that works with HTML data, CSS helps to style that data.  In this example, we are using JavaScript and CSS that was developed by others (3rd party).  Addithing the 3rd party code makes the table interactive.
- Look at the href and src on lines inside of the lines in `<head>` tags.  This is adding code to our page from others.
- Observe the `<script>` tags at the bottom of the page.  This is generating the interactive table, from the third party code, using the data `<table id="demo">` from the `<body>`.  
- Benefits of a markdown table include, more simplicity, aswell it being easier to read
- HTML (Hypertext Markup Language) is a markup language used for structuring content on the web, while JavaScript is a scripting language that enables interactivity and dynamic behavior within web pages.
- A table using JavaScript can dynamically sort and filter data, improving user experience and data accessibility.

## Hacks
This lesson teaches you about tables.  In this hack, it is important that you analze the difference in the styles of output shown.  
- Make your own tables, with data according to your interests.
- Describe a benefit of a markdown table.
- Try to Style the HTML table using w3schools.
- Describe the difference between HTML and JavaScript.
- Describe a benefit of a table that uses JavaScript.

