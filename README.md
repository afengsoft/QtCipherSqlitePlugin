QtCipherSqlitePlugin
====================

A Qt plugin for cipher SQLite which is based on SQLite source and wxSQLite3 in wxWidget.

Qt is a full development framework with tools designed to streamline the creation of applications and user interfaces for desktop, embedded and mobile platforms. You could find more details at https://www.qt.io.

SQLite is a software library that implements a self-contained, serverless, zero-configuration, transactional SQL database engine. SQLite is the most widely deployed SQL database engine in the world. The source code for SQLite is in the public domain. You could find more details at http://www.sqlite.org/.

wxSQLite3 is a C++ wrapper around the public domain SQLite 3.x database and is specifically designed for use in programs based on the wxWidgets library. wxSQLite3 includes an optional extension for SQLite supporting key based database file encryption using 128 bit AES encryption. You could find more details at http://utelle.github.io/wxsqlite3. wxSQLite3 is released under wxWindows Library Licence.

You could find how to compile this plugin at http://qtciphersqliteplugin.galaxyworld.org.

Please read [Wiki](https://github.com/devbean/QtCipherSqlitePlugin/wiki) for more details.

使用插件
加密数据库
QSqlDatabase dbconn = QSqlDatabase::addDatabase("SQLITECIPHER");
dbconn.setDatabaseName("test.db");
dbconn.setPassword("test");
//将原本没有加密的数据库文件进行加密，此代码只需执行一次
dbconn.setConnectOptions("QSQLITE_CREATE_KEY");
dbconn.open()

删除数据库密码
//其他代码不变，只需要修改这一句就可以了
dbconn.setConnectOptions("QSQLITE_REMOVE_KEY");
修改数据库密码
//其他代码不变，只需要修改这一句在后面加上新的密码即可
dbconn.setConnectOptions("QSQLITE_UPDATE_KEY=newtest");
//等同于删除密码
dbconn.setConnectOptions("QSQLITE_UPDATE_KEY=");
运行时设置加密算法
/*
QSQLITE_USE_CIPHER的可选值分别为：
	aes128cbc		AES 128 Bit CBC – No HMAC (wxSQLite3)
	aes256cbc		AES 256 Bit CBC – No HMAC (wxSQLite3)
	chacha20		ChaCha20 – Poly1305 – Poly1305 HMAC (sqleet)
	sqlcipher		AES 256 Bit CBC – SHA1 HMAC (SQLCipher)
*/
dbconn.setConnectOptions("QSQLITE_USE_CIPHER=sqlcipher");
