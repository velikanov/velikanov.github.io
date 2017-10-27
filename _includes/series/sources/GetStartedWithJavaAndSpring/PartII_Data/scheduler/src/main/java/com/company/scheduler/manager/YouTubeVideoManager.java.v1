package com.company.scheduler.manager;

import com.company.scheduler.properties.SchedulerProperties;
import com.google.api.client.http.HttpRequest;
import com.google.api.client.http.HttpRequestInitializer;
import com.google.api.client.http.javanet.NetHttpTransport;
import com.google.api.client.json.jackson2.JacksonFactory;
import com.google.api.services.youtube.YouTube;
import com.google.api.services.youtube.YouTubeRequestInitializer;
import com.google.api.services.youtube.model.Video;
import com.google.api.services.youtube.model.VideoListResponse;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

import java.io.IOException;
import java.util.ArrayList;
import java.util.List;

@Component
public class YouTubeVideoManager {
    private YouTube youTube;

    @Autowired
    public YouTubeVideoManager(SchedulerProperties schedulerProperties) {
        youTube = new YouTube.Builder(
                new NetHttpTransport(),
                new JacksonFactory(),
                new HttpRequestInitializer() {
                    @Override
                    public void initialize(HttpRequest httpRequest) throws IOException {

                    }
                }
        ).setYouTubeRequestInitializer(new YouTubeRequestInitializer(schedulerProperties.getYouTubeApiKey())).build();
    }

    public List<Video> getRecentTrendingVideoList()
    {
        try {
            YouTube.Videos.List youTubeVideosList = youTube.videos().list("contentDetails,snippet");
            youTubeVideosList.setChart("mostPopular");

            VideoListResponse youtubeVideosListResponse = youTubeVideosList.execute();

            return youtubeVideosListResponse.getItems();
        } catch (IOException e) {
            e.printStackTrace();

            return new ArrayList<>();
        }
    }
}