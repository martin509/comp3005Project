CREATE TABLE Author
	(author_id	varchar(8),
	author_name	varchar(20) NOT NULL,
	author_email	varchar(20),
	PRIMARY KEY (author_id)
	);

CREATE TABLE AuthorList
	(author_id	varchar(8),
	alist_id	varchar(8),
	PRIMARY KEY (author_id, alist_id),
	FOREIGN KEY (author_id) REFRENCES Author
	);

CREATE TABLE PubPhone
	(pubphone_id 	varchar(8),
	number		numeric(11,0),
	PRIMARY KEY (pubphone_id, number)
	);

CREATE TABLE Address
	(addr_id	varchar(8),
	street_number	numeric(4,0),
	street_name	varchar(20),
	city		varchar(20),
	province	varchar(20),
	postal_code	varchar(6)
	PRIMARY KEY (addr_id)
	);

CREATE TABLE BankAccount
	(acc_id		varchar(8),
	amount		numeric
	PRIMARY KEY (acc_id)
	);

CREATE TABLE Publisher
	(pub_id		varchar(8),
	pub_name	varchar(20) NOT NULL,
	pub_email	varchar(20),
	addr_id		varchar(8),
	acc_id		varchar(8),
	pubphone_id	varchar(8),
	PRIMARY KEY (pub_id),
	FOREIGN KEY (addr_id) REFERENCES Address,
	FOREIGN KEY (acc_id) REFERENCES BankAccount,
	FOREIGN KEY (pubphone_id) REFERENCES PubPhone
	);

CREATE TABLE Book
	(ISBN		numeric(13),
	n_pages		numeric(4,0) NOT NULL,
	title		varchar(20) NOT NULL,
	price		numeric(5,2) NOT NULL,
	percentage	numeric(2,2) NOT NULL,
	genre_name	varchar(20),
	pub_id		varchar(8),
	alist_id	varchar(8)
	PRIMARY KEY (ISBN),
	FOREIGN KEY (pub_id) REFERENCES Publisher,
	FOREIGN KEY (alist_id) REFERENCES AuthorList
	);

CREATE TABLE User
	(user_id	varchar(8),
	user_name	varchar(20) NOT NULL,
	user_email	varchar(20) NOT NULL,
	PRIMARY KEY (user_id)
	);

CREATE TABLE UserAccount
	(user_id	varchar(8),
	acc_id		varchar(8),
	PRIMARY KEY (user_id),
	FOREIGN KEY (user_id) references User,
	FOREIGN KEY (acc_id) REFERENCES BankAccount
	);

CREATE TABLE BasketEntry
	(ISBN		varchar(8),
	basket_id	varchar(8),
	bookCount	numeric(2,0) NOT NULL,
	PRIMARY KEY(ISBN, basket_id),
	FOREIGN KEY(ISBN) REFERENCES Book,
	FOREIGN KEY(basket_id) REFERENCES Basket
	);

CREATE TABLE Basket
	(basket_id	varchar(8),
	user_id		varchar(8),
	PRIMARY KEY (basket_id),
	FOREIGN KEY (user_id) REFERENCES User
	);

CREATE TABLE Order
	(location	varchar(20),
	addr_id		varchar(8),
	basket_id	varchar(8),
	PRIMARY KEY (basket_id),
	FOREIGN KEY (basket_id) REFERENCES Basket,
	FOREIGN KEY (addr_id) REFERENCES Address
	);