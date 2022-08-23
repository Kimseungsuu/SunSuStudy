**Interface 란?**

- **JPA는 Repository를 통해서만 사용할 수 있습니다.**
- 인터페이스는 클래스에서 멤버가 빠진, 메소드 모음집이라고 보시면 됩니다.

  ![](C:/Users/User/Desktop/Untitled.png)


```sql
public interface CourseRepository extends JpaRepository<Course, Long> { //extends 상속 다른기능을 내가 뒤에 있는 JpaRepository 가져와서 courseRepository 쓸꺼야

}
```

→ JpaRepository 는 interface 라는 이야기인데

→ JpaRepository 멤버변수 이런건 없고 메소드가 잔뜩 놓여 있는 녀석 이구나

→ CourseRepository 마찬가지로 메소드만 잔뜩 모여있는 녀석

→ 그메소드는 내가 작성하는게 아니고 JpaRepository 미리작성된 것을 내가 가져다쓰는거구나

- JpaRepository

    ```java
    /*
     * Copyright 2008-2022 the original author or authors.
     *
     * Licensed under the Apache License, Version 2.0 (the "License");
     * you may not use this file except in compliance with the License.
     * You may obtain a copy of the License at
     *
     *      https://www.apache.org/licenses/LICENSE-2.0
     *
     * Unless required by applicable law or agreed to in writing, software
     * distributed under the License is distributed on an "AS IS" BASIS,
     * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
     * See the License for the specific language governing permissions and
     * limitations under the License.
     */
    package org.springframework.data.jpa.repository;
    
    import java.util.List;
    
    import javax.persistence.EntityManager;
    
    import org.springframework.data.domain.Example;
    import org.springframework.data.domain.Sort;
    import org.springframework.data.repository.NoRepositoryBean;
    import org.springframework.data.repository.PagingAndSortingRepository;
    import org.springframework.data.repository.query.QueryByExampleExecutor;
    
    /**
     * JPA specific extension of {@link org.springframework.data.repository.Repository}.
     *
     * @author Oliver Gierke
     * @author Christoph Strobl
     * @author Mark Paluch
     * @author Sander Krabbenborg
     * @author Jesse Wouters
     * @author Greg Turnquist
     */
    @NoRepositoryBean
    public interface JpaRepository<T, ID> extends PagingAndSortingRepository<T, ID>, QueryByExampleExecutor<T> {
    
    	/*
    	 * (non-Javadoc)
    	 * @see org.springframework.data.repository.CrudRepository#findAll()
    	 */
    	@Override
    	List<T> findAll();
    
    	/*
    	 * (non-Javadoc)
    	 * @see org.springframework.data.repository.PagingAndSortingRepository#findAll(org.springframework.data.domain.Sort)
    	 */
    	@Override
    	List<T> findAll(Sort sort);
    
    	/*
    	 * (non-Javadoc)
    	 * @see org.springframework.data.repository.CrudRepository#findAll(java.lang.Iterable)
    	 */
    	@Override
    	List<T> findAllById(Iterable<ID> ids);
    
    	/*
    	 * (non-Javadoc)
    	 * @see org.springframework.data.repository.CrudRepository#save(java.lang.Iterable)
    	 */
    	@Override
    	<S extends T> List<S> saveAll(Iterable<S> entities);
    
    	/**
    	 * Flushes all pending changes to the database.
    	 */
    	void flush();
    
    	/**
    	 * Saves an entity and flushes changes instantly.
    	 *
    	 * @param entity entity to be saved. Must not be {@literal null}.
    	 * @return the saved entity
    	 */
    	<S extends T> S saveAndFlush(S entity);
    
    	/**
    	 * Saves all entities and flushes changes instantly.
    	 *
    	 * @param entities entities to be saved. Must not be {@literal null}.
    	 * @return the saved entities
    	 * @since 2.5
    	 */
    	<S extends T> List<S> saveAllAndFlush(Iterable<S> entities);
    
    	/**
    	 * Deletes the given entities in a batch which means it will create a single query. This kind of operation leaves JPAs
    	 * first level cache and the database out of sync. Consider flushing the {@link EntityManager} before calling this
    	 * method.
    	 *
    	 * @param entities entities to be deleted. Must not be {@literal null}.
    	 * @deprecated Use {@link #deleteAllInBatch(Iterable)} instead.
    	 */
    	@Deprecated
    	default void deleteInBatch(Iterable<T> entities) {
    		deleteAllInBatch(entities);
    	}
    
    	/**
    	 * Deletes the given entities in a batch which means it will create a single query. This kind of operation leaves JPAs
    	 * first level cache and the database out of sync. Consider flushing the {@link EntityManager} before calling this
    	 * method.
    	 *
    	 * @param entities entities to be deleted. Must not be {@literal null}.
    	 * @since 2.5
    	 */
    	void deleteAllInBatch(Iterable<T> entities);
    
    	/**
    	 * Deletes the entities identified by the given ids using a single query. This kind of operation leaves JPAs first
    	 * level cache and the database out of sync. Consider flushing the {@link EntityManager} before calling this method.
    	 *
    	 * @param ids the ids of the entities to be deleted. Must not be {@literal null}.
    	 * @since 2.5
    	 */
    	void deleteAllByIdInBatch(Iterable<ID> ids);
    
    	/**
    	 * Deletes all entities in a batch call.
    	 */
    	void deleteAllInBatch();
    
    	/**
    	 * Returns a reference to the entity with the given identifier. Depending on how the JPA persistence provider is
    	 * implemented this is very likely to always return an instance and throw an
    	 * {@link javax.persistence.EntityNotFoundException} on first access. Some of them will reject invalid identifiers
    	 * immediately.
    	 *
    	 * @param id must not be {@literal null}.
    	 * @return a reference to the entity with the given identifier.
    	 * @see EntityManager#getReference(Class, Object) for details on when an exception is thrown.
    	 * @deprecated use {@link JpaRepository#getReferenceById(ID)} instead.
    	 */
    	@Deprecated
    	T getOne(ID id);
    
    	/**
    	 * Returns a reference to the entity with the given identifier. Depending on how the JPA persistence provider is
    	 * implemented this is very likely to always return an instance and throw an
    	 * {@link javax.persistence.EntityNotFoundException} on first access. Some of them will reject invalid identifiers
    	 * immediately.
    	 *
    	 * @param id must not be {@literal null}.
    	 * @return a reference to the entity with the given identifier.
    	 * @see EntityManager#getReference(Class, Object) for details on when an exception is thrown.
    	 * @deprecated use {@link JpaRepository#getReferenceById(ID)} instead.
    	 * @since 2.5
    	 */
    	@Deprecated
    	T getById(ID id);
    
    	/**
    	 * Returns a reference to the entity with the given identifier. Depending on how the JPA persistence provider is
    	 * implemented this is very likely to always return an instance and throw an
    	 * {@link javax.persistence.EntityNotFoundException} on first access. Some of them will reject invalid identifiers
    	 * immediately.
    	 *
    	 * @param id must not be {@literal null}.
    	 * @return a reference to the entity with the given identifier.
    	 * @see EntityManager#getReference(Class, Object) for details on when an exception is thrown.
    	 * @since 2.7
    	 */
    	T getReferenceById(ID id);
    
    	/*
    	 * (non-Javadoc)
    	 * @see org.springframework.data.repository.query.QueryByExampleExecutor#findAll(org.springframework.data.domain.Example)
    	 */
    	@Override
    	<S extends T> List<S> findAll(Example<S> example);
    
    	/*
    	 * (non-Javadoc)
    	 * @see org.springframework.data.repository.query.QueryByExampleExecutor#findAll(org.springframework.data.domain.Example, org.springframework.data.domain.Sort)
    	 */
    	@Override
    	<S extends T> List<S> findAll(Example<S> example, Sort sort);
    }
    ```