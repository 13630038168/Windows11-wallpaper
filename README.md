@@ -8,6 +8,8 @@

import com.alibaba.fastjson.JSON;
import com.alibaba.fastjson.JSONArray;
import com.alibaba.fastjson2.JSONObject;
import com.alibaba.fastjson2.JSONWriter.Feature;

import com.wdbyte.bing.BingFileUtils;
import com.wdbyte.bing.Images;
@@ -50,8 +52,14 @@ public void htmlGenerator() throws IOException {

    private void htmlGeneratorToday(List<Images> bingImages) throws IOException {
        String url = bingImages.get(0).getUrl();
        String fileName = String.format("%s-%s.jpg", Wallpaper.CURRENT_REGION, bingImages.get(0).getDate());
        HtmlFileUtils.writeToday(fileName + ":" + url);
        String fileName = String.format("%s_%s.jpg", Wallpaper.CURRENT_REGION, bingImages.get(0).getDate());
        JSONObject jsonObject = new JSONObject();
        jsonObject.put("file_name", fileName);
        jsonObject.put("url", url);
        jsonObject.put("date", bingImages.get(0).getDate());
        jsonObject.put("region", Wallpaper.CURRENT_REGION);
        jsonObject.put("desc", bingImages.get(0).getDesc());
        HtmlFileUtils.writeToday(jsonObject.toString(Feature.PrettyFormat));
    }

    public void htmlGeneratorIndex(List<Images> bingImages, Map<String, List<Images>> monthMap) throws IOException {
