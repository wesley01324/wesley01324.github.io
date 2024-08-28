### 以一个获取生产订单为示例

```
public async Task<ProPlan[]> GetPlan()
{
    ProPlan[] plan;
    string baseUrl = "http://192.168.2.93:2000/api/json/Read";
    using (HttpClient client = new HttpClient())
    {
        try
        {
            HttpResponseMessage response = await client.GetAsync(baseUrl);
            response.EnsureSuccessStatusCode();
            string responseData = await response.Content.ReadAsStringAsync();
            var json = JsonConvert.DeserializeObject(responseData);
            plan = JsonConvert.DeserializeObject<ProPlan[]>(json.ToString());
            return plan;
        }
        catch (Exception ex)
        {
            Trace.WriteLine(ex.Message);
            return InitData;
        }
    };
}
```