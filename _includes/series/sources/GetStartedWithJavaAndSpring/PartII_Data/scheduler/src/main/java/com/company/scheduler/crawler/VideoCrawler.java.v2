package com.company.scheduler.crawler;

import com.company.library.domain.Video;
import com.company.library.domain.VideoRepository;
import com.company.scheduler.manager.VideoManager;
import com.company.scheduler.manager.YouTubeVideoManager;
import com.company.scheduler.properties.SchedulerProperties;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

import java.util.List;

@Component
public class VideoCrawler implements Crawler {
    private final VideoManager videoManager;
    private final YouTubeVideoManager youTubeVideoManager;
    private final VideoRepository videoRepository;
    private final SchedulerProperties schedulerProperties;

    @Autowired
    public VideoCrawler(
            VideoManager videoManager,
            YouTubeVideoManager youTubeVideoManager,
            VideoRepository videoRepository,
            SchedulerProperties schedulerProperties
    ) {
        this.videoManager = videoManager;
        this.youTubeVideoManager = youTubeVideoManager;
        this.videoRepository = videoRepository;
        this.schedulerProperties = schedulerProperties;
    }

    @Override
    public void crawl() {
        System.out.println("New videos crawling started");

        List<com.google.api.services.youtube.model.Video> recentTrendingVideoList =
                youTubeVideoManager.getRecentTrendingVideoList();

        for (com.google.api.services.youtube.model.Video youtubeVideo : recentTrendingVideoList) {
            if (null != videoRepository.findByExternalId(youtubeVideo.getId())) {
                break;
            }

            Video video = videoManager.createFromYoutubeVideo(youtubeVideo);

            videoRepository.save(video);

            System.out.println(String.format("Video %s (%s) saved", video.getTitle(), video.getExternalId()));
        }

        System.out.println("New videos crawling ended");
    }
}