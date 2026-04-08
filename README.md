# Metro Report Analytics Dashboard — Assignment 5 

## CSV & PapaParse 

A CSV file is just a plain text file where each line is a row of data and each value is separated by a comma; hence "comma-separated values." Weird, right? Browsers and JavaScript have no built in way to parse these cleanly, which is i think where PapaParse comes in. From my research and testing, PapaParse reads the file, splits it into rows, uses the first row as field names, and hands back a JavaScript array of objects where each object is one row and each key is a column name. The dynamicTyping: true option tells PapaParse to convert number strings into actual JavaScript numbers automatically as without it, "4850" stays a string and doing math on it produces NaN instead of a number, which would break every calculation in the dashboard. For my own environment, I also needed the download=true option as Edge enforced CORS in my Enterprise Environment and the solution was not quick enough for me. 

## KPI Calculation 

.reduce() is a JavaScript array method that collapses an array down to a single value by running a function on each element and carrying a running result forward. For summing sessions across 30 rows, it starts at zero and adds each row's session count one at a time until it has processed every row and returns the total. It is the right tool here because KPIs are by definition aggregations — you are collapsing many rows into one number. The alternative would be a for loop with a running variable, which works but is more verbose. For averages, .reduce() gives the sum and then dividing by rows.length gives the mean. The bounce rate and conversion rate averages work this way since you want the average across all 30 rows, not a sum. 

## Chart Types 

The bar chart works for sessions and revenue by source because the question is a comparison, like how does Organic stack up against Paid, Social, Email, and Referral? Bar charts are the standard answer when you are comparing discrete categories against each other and the exact values matter. 

The doughnut chart works for revenue share because the question is about proportion: What percentage of total revenue does each source contribute? Pie and doughnut charts show part to whole relationships, which is exactly what "share" means. A bar chart would answer a different question. 

The line chart works for the monthly trend because the question is about change over time; such as are sessions growing, are they flat, or are they dropping for each source across six months? Lines connect data points across a time axis and make it easy to see trajectory. Using a bar chart for this would make it much harder to follow any single source across the months since you would have five bars clustered at each month. 

## Real-World Reflection 

Organic search is the clear top performer across sessions, revenue, and new visitors. You can see how it is growing the fastest, going from 4,850 sessions in January to 7,100 in June. Email has the lowest session count of any source but consistently the highest conversion rate, which tells the editorial team that email subscribers are the most engaged and valuable audience even if they are the smallest group. Social drives decent volume but has the worst bounce rate by far, suggesting those visitors are arriving and not finding what they expected, then leaving. The dashboard helps an editor make decisions because it surfaces these patterns in one place rather than requiring them to read a spreadsheet. Though, of course its worth noting that in most cases people in management at this point still prefer the spreadsheets; it tends to be shareable! 
