# leetcode-streak

Quick check of LeetCode streak stats for username `abhyas29`.

## Usage

```bash
python3 -c 'import urllib.request,json,time,itertools as it;req=urllib.request.Request("https://leetcode.com/graphql",data=json.dumps({"query":"query{matchedUser(username:\"abhyas29\"){userCalendar{totalActiveDays submissionCalendar}}}"}).encode(),headers={"Content-Type":"application/json","User-Agent":"Mozilla/5.0"});d=json.loads(urllib.request.urlopen(req).read())["data"]["matchedUser"]["userCalendar"];days=sorted({int(k)//86400 for k,v in json.loads(d["submissionCalendar"]).items() if v>0});groups=[list(g) for _,g in it.groupby(enumerate(days),key=lambda t:t[1]-t[0])];longest=max((len(g) for g in groups),default=0);today=int(time.time())//86400;current=len(groups[-1]) if days and days[-1]==today else 0;print({"current_streak":current,"active_days":d["totalActiveDays"],"longest_streak":longest})'
```

Output:

```
{'current_streak': 1, 'active_days': 11, 'longest_streak': 6}
```

- `current_streak` — consecutive days up to and including today with at least one submission
- `active_days` — total all-time days with at least one submission
- `longest_streak` — longest consecutive-day run ever recorded
