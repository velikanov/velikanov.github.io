package com.company.scheduler.manager;

import com.company.library.domain.Video;
import com.google.api.services.youtube.model.Thumbnail;
import com.google.api.services.youtube.model.ThumbnailDetails;
import com.google.api.services.youtube.model.VideoContentDetails;
import com.google.api.services.youtube.model.VideoSnippet;
import org.springframework.stereotype.Component;

@Component
public class VideoManager {
    public Video createFromYoutubeVideo(com.google.api.services.youtube.model.Video youtubeVideo) {
        VideoSnippet youtubeVideoSnippet = youtubeVideo.getSnippet();
        VideoContentDetails youtubeVideoContentDetails = youtubeVideo.getContentDetails();

        Video video = new Video();
        video.setExternalId(youtubeVideo.getId());

        if (null != youtubeVideoSnippet) {
            video.setTitle(youtubeVideoSnippet.getTitle());

            ThumbnailDetails youtubeVideoThumbnailDetails = youtubeVideoSnippet.getThumbnails();
            if (youtubeVideoThumbnailDetails.size() > 0) {
                video.setImageUri(resolveThumbnailUrl(youtubeVideoThumbnailDetails));
            }
        }

        if (null != youtubeVideoContentDetails) {
            video.setDuration(youtubeVideo.getContentDetails().getDuration());
        }

        return video;
    }

    private String resolveThumbnailUrl(ThumbnailDetails thumbnailDetails) {
        Thumbnail thumbnail = thumbnailDetails.getMaxres();
        if (null != thumbnail) {
            return thumbnail.getUrl();
        }

        thumbnail = thumbnailDetails.getHigh();
        if (null != thumbnail) {
            return thumbnail.getUrl();
        }

        thumbnail = thumbnailDetails.getMedium();
        if (null != thumbnail) {
            return thumbnail.getUrl();
        }

        thumbnail = thumbnailDetails.getStandard();
        if (null != thumbnail) {
            return thumbnail.getUrl();
        }

        thumbnail = thumbnailDetails.getDefault();
        if (null != thumbnail) {
            return thumbnail.getUrl();
        }

        return null;
    }
}