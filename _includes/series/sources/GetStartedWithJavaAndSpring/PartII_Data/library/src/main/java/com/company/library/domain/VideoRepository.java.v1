package com.company.library.domain;

import org.springframework.data.domain.Page;
import org.springframework.data.domain.Pageable;
import org.springframework.data.jpa.repository.Query;
import org.springframework.data.repository.CrudRepository;

import java.util.List;

public interface VideoRepository extends CrudRepository<Video, Integer> {
    Page<Video> findAllByOrderByCreatedDateDescExternalIdDesc(Pageable pageable);
    Page<Video> findAllByOrderByDurationDesc(Pageable pageable);
    @Query(value = "SELECT * FROM video ORDER BY RAND() LIMIT 0, ?1", nativeQuery = true)
    List<Video> findPagedByRand(int pageSize);
}