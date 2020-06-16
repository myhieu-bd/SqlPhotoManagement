# Create tables

## Create table users
```
CREATE TABLE users (
    id int PRIMARY KEY AUTO_INCREMENT NOT NULL,
	email VARCHAR(50),
	password VARCHAR(50),
	role VARCHAR(50),
	created_at DATETIME,
	updated_at DATETIME     
);
```

## Create table categories
```
CREATE TABLE categories(
	id int PRIMARY KEY AUTO_INCREMENT NOT NULL,
	name VARCHAR(50),
	created_at DATETIME,
	updated_at DATETIME 
);
```

## Create table photos
```
CREATE TABLE photos(
	id int PRIMARY KEY AUTO_INCREMENT NOT NULL,
	title VARCHAR(100),
	category_id INT,
	image VARCHAR(100),
	created_at DATETIME,
	updated_at DATETIME,
	FOREIGN KEY (category_id) REFERENCES categories(id)
);
```

## Create table tags
```
CREATE TABLE tags(
	id int PRIMARY KEY NOT NULL AUTO_INCREMENT,
	name VARCHAR(50),
	created_at DATETIME,
	updated_at DATETIME 
);
```

## Create table taggable
```
CREATE TABLE taggable(
	tag_id int,
    photo_id int
	FOREIGN KEY (tag_id) REFERENCES tags(id),
    FOREIGN KEY (photo_id) REFERENCES photos(id)
	created_at DATETIME,
	updated_at DATETIME 
);
```

## Create table photo_descriptions
```
CREATE TABLE photo_descriptions(
	photo_id int NOT NULL,
	content VARCHAR(50),
	created_at DATETIME,
	updated_at DATETIME,
	FOREIGN KEY (photo_id) REFERENCES photos(id),
	PRIMARY KEY (photo_id)
);
```
# Inserts

## users
```
INSERT INTO users (email, password, role)
VALUES  ('abc@gmail.com', '123', 'user'), 
        ('admin@gmail.com', '321', 'admin');
```

## categories
```
INSERT INTO categories (name)
VALUES  ('anh chan dung'), ('phong canh'), ('bien');
        
```

## photos
```
INSERT INTO photos (title, category_id, image)
VALUES  ('ảnh hiệu', 1, 'hieu.png'),
        ('hoàng hôn trên biển', '3', 'hoanghon.png');
        
```
## tags
```
INSERT INTO taggable (name)
VALUES  ('hoàng hôn'),(' bình minh'), ('chiều tà'),
        ('hoàng hôn trên biển'), ('đồi hoa'), ('chân trời');
        
```

## taggable
```
INSERT INTO taggable (tag_id, photo_id)
VALUES  (3, 1),
        (2,2),
        (1,1), 
        (5,2),
        (4,1);
      
        
```

## photo_descriptions
```
INSERT INTO photo_descriptions (photo_id, content)
VALUES  (1,'xinh đẹp quá đi à');
        
```

# Query
```
SELECT photos.title, photos.image, photo_descriptions.content
FROM photos
INNER JOIN photo_descriptions ON photos.id=photo_descriptions.photo_id;

SELECT photos.title, photos.image, photo_descriptions.content
FROM photos
LEFT JOIN photo_descriptions ON photos.id=photo_descriptions.photo_id
ORDER BY photos.title;

```