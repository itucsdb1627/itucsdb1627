Geliştirici Kılavuzu
====================

Veritabanı Dizaynı
------------------

   Projemizin veritabanı dizaynı ayrı ayrı gerçeklenmiştir. Her takım elemanı kendi veritabanını dizayn etmiştir.

   Bu yüzden, veritabanı dizaynı ve E/R diyagramı ayrı olarak ele alınacaktır.

   Veritabanı tablolarımız ElephantSQL'de tutulmaktadır.

   Projemizde sorgulama dili olarak PostgreSQL kullanılmıştır.

1. Burak Şimşek'in Veritabanı ve E/R diagramı
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


1.1. Veritabanı Dizaynı
"""""""""""""""""""""""

Maindata tablosu 5 niteliğe sahiptir. Bu nitelikler ID,email,password,name ve surname olarak adlandırılmışlardır.ID değeri sadece
sistemde kullanılmaktadır. Maindata tablosunun yaratılması için gerekli kod aşağıda verilmiştir.

.. code-block:: sql

   CREATE TABLE MAINDATA(ID SERIAL PRIMARY KEY, EMAIL VARCHAR(50) NOT NULL,
      PASSWORD VARCHAR(50) NOT NULL,NAME VARCHAR(50) NOT NULL,SURNAME VARCHAR(50)
      NOT NULL,UNIQUE(EMAIL))

FriendRequest tablosu 2 niteliğe sahiptir.Bu nitelikler personid ve friendrequestid olarak adlandırılmıştır.Bu tablo personid
dış anahtarı ile Maindata tablosuna bağlıdır. FriendRequest tablosunun yaratılması için gerekli kod aşağıda verilmiştir.

.. code-block::   sql

   CREATE TABLE FRIENDREQUEST
   (PERSONID INTEGER,REQUESTID INTEGER,
   FOREIGN KEY (PERSONID) REFERENCES MAINDATA(ID) ON
   DELETE CASCADE ON UPDATE CASCADE )




FriendList tablosu 3 niteliğe sahiptir.Bu nitelikler personid,friendid ve title olarak adlandırılmıştır.Bu tablo personid
dış anahtarı ile Maindata tablosuna bağlıdır. FriendList tablosunun yaratılması için gerekli kod aşağıda verilmiştir.

.. code-block:: sql

    CREATE TABLE FRIENDLIST(PERSONID INTEGER,FRIENDID INTEGER,TITLE VARCHAR(50),
    FOREIGN KEY (PERSONID) REFERENCES MAINDATA(ID)
    ON DELETE CASCADE ON UPDATE CASCADE )




1.2. E/R Diyagramı
""""""""""""""""""

Yukarıdaki tablolar için oluşturulan ER diagramı aşağıda verilmiştir.

.. figure:: Burak/BurakER.png
      :scale: 100 %
      :alt:

      *Maindata,FriendRequest,FriendList tabloları için E/R Diyagramı*




2. Zihnican Beğburs'un Veritabanı ve E/R Diagramı
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.1. Database Design
""""""""""""""""""""

Education tablosu 6 niteliğe sahiptir. Bu nitelikler ID,SCHOOLNAME,YEARSTART,YEAREND,PERSONID ve GPA dir. Bu tablo personid
dış anahtarı ile Maindata tablosuna bağlıdır. Education tablosunun yaratılması için gerekli kod aşağıda verilmiştir.
.. code-block:: sql

                CREATE TABLE IF NOT EXISTS EDUCATION (
                ID SERIAL PRIMARY KEY,
                SCHOOLNAME VARCHAR(90),
                YEARSTART VARCHAR(30) NULL,
                YEAREND VARCHAR(30) NULL,
                PERSONID INTEGER,
                GPA VARCHAR(30) NULL,
                FOREIGN KEY (PERSONID)
                REFERENCES MAINDATA (ID)
                ON DELETE CASCADE)


Experience tablosu 6 niteliğe sahiptir. Bu nitelikler ID,COMPANYNAME,YEARSTART,YEAREND,POSITION ve PERSONID dir. Bu tablo personid
dış anahtarı ile Maindata tablosuna bağlıdır. Experience tablosunun yaratılması için gerekli kod aşağıda verilmiştir.



    .. code-block:: sql

            CREATE TABLE IF NOT EXISTS EXPERIENCE (
            ID SERIAL PRIMARY KEY,
            COMPANYNAME VARCHAR(90),
            YEARSTART VARCHAR(30) NULL,
            YEAREND VARCHAR(30) NULL,
            POSITION VARCHAR(30) NULL,
            PERSONID INTEGER,
            FOREIGN KEY (PERSONID)
            REFERENCES MAINDATA (ID)
            ON DELETE CASCADE)

Language tablosu 4 niteliğe sahiptir. Bu nitelikler ID,LANGUAGENAME,LEVEL ve PERSONID dir. Bu tablo personid
dış anahtarı ile Maindata tablosuna bağlıdır. Language tablosunun yaratılması için gerekli kod aşağıda verilmiştir.


      .. code-block:: sql

            CREATE TABLE IF NOT EXISTS LANGUAGE (
            ID SERIAL PRIMARY KEY,
            LANGUAGENAME VARCHAR(90),
            LEVEL VARCHAR(30) NULL,
            PERSONID INTEGER,
            FOREIGN KEY (PERSONID)
            REFERENCES MAINDATA (ID)
            ON DELETE CASCADE)

2.2. E/R Diyagramı
""""""""""""""""""

   Yukarıdaki tablolar için oluşturulan ER diagramı aşağıda verilmiştir:

.. figure:: Zihni/ERDiyagramZihni.jpg
      :scale: 100 %
      :alt:

      *Education,Language,Experience tabloları için E/R Diyagramı.*







3. Hilal Gülşen'in Veritabanı ve E/R diagramı
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.1. Veritabanı Dizaynı
"""""""""""""""""""""""
GRUP tablosu 6 niteliğe sahiptir. ID, GROUPNAME, EXPLANATION, STARTDATE, SECTOR, PERSONID bu tablonun nitelikleridir. ID ve PERSONID değerleri kullanıcıya görünmemektedir. Bu tablo PERSONID dış anahtarı ile MAINDATA tablosuna bağlıdır. GRUP tablosu aşağıdaki SQL kodu ile yaratılmaktadır:

        .. code-block:: sql

                 CREATE TABLE IF NOT EXISTS GRUP (
                 ID SERIAL PRIMARY KEY,
                 GROUPNAME VARCHAR(90) NOT NULL,
                 EXPLANATION VARCHAR(400) NOT NULL,
                 STARTDATE DATE NOT NULL,
                 SECTOR VARCHAR(90) NOT NULL,
                 PERSONID INTEGER,
                 FOREIGN KEY (PERSONID)
                 REFERENCES MAINDATA (ID)
                 ON DELETE CASCADE)

PUBLISHES tablosu 6 niteliğe sahiptir. ID, ESSAYTYPE, PUBLISHNAME, PUBLISHCONTENT, PUBLISHDATE, PERSONID bu tablonun nitelikleridir. ID ve PERSONID değerleri kullanıcıya görünmemektedir. Bu tablo PERSONID dış anahtarı ile MAINDATA tablosuna bağlıdır. PUBLISHES tablosu aşağıdaki SQL kodu ile yaratılmaktadır:

    .. code-block:: sql

             CREATE TABLE IF NOT EXISTS PUBLISHES (
             ID SERIAL PRIMARY KEY,
             ESSAYTYPE VARCHAR(90) NOT NULL,
             PUBLISHNAME VARCHAR(90) NOT NULL,
             PUBLISHCONTENT VARCHAR(500) NOT NULL,
             PUBLISHDATE DATE NOT NULL,
             PERSONID INTEGER,
             FOREIGN KEY (PERSONID)
             REFERENCES MAINDATA (ID)
             ON DELETE CASCADE)

ACTIVITIES tablosu 5 niteliğe sahiptir. ID, ACTIVITYNAME, ACTIVITYCONTENT, ACTIVITYDATE, PERSONID bu tablonun nitelikleridir. ID ve PERSONID değerleri kullanıcıya görünmemektedir. Bu tablo PERSONID dış anahtarı ile MAINDATA tablosuna bağlıdır. ACTIVITIES tablosu aşağıdaki SQL kodu ile yaratılmaktadır:


      .. code-block:: sql

             CREATE TABLE IF NOT EXISTS ACTIVITIES (
             ID SERIAL PRIMARY KEY,
             ACTIVITYNAME VARCHAR(150) NOT NULL,
             ACTIVITYCONTENT VARCHAR(400) NOT NULL,
             ACTIVITYDATE DATE NOT NULL,
             PERSONID INTEGER,
             FOREIGN KEY (PERSONID)
             REFERENCES MAINDATA (ID)
             ON DELETE CASCADE)


3.2. E/R Diyagram
"""""""""""""""""

   Tablolarım için E/R diyagramı :

   .. figure:: Hilal/ERDiyagrami.jpg
      :scale: 100 %
      :alt:

      *Grup, Publishes, Activities tabloları için E/R Diyagramı*


4. Zeynep Ankara' nın Veritabanı ve E/R diagramı
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

4.1. Veritabanı Dizaynı
"""""""""""""""""""""""
NETWORK tablosu 5 niteliğe sahiptir. ID, IL, SIRKET, SEKTOR, PERSONID bu tablonun nitelikleridir. Bu tablo PERSONID dış anahtarı ile MAINDATA tablosuna bağlıdır. NETWORK tablosu aşağıdaki SQL kodu ile oluşturulmuştur:



		.. code-block:: sql

		 CREATE TABLE IF NOT EXISTS NETWORK (
    	         ID SERIAL PRIMARY KEY,
    	         IL VARCHAR(90),
    	         SIRKET VARCHAR(30) NULL,
    	         PERSONID INTEGER,
    	         SEKTOR VARCHAR(30) NULL,
    	         FOREIGN KEY (PERSONID)
    	         REFERENCES MAINDATA (ID)
    	         ON DELETE CASCADE)


4.2. E/R Diyagram
"""""""""""""""""


	Oluşturulan Network Tablosuna ait E/R diyagramı aşağıdaki gibidir;

	.. figure:: Zeynep/ERDiyagram.jpg




Kod
---

   Veritabanı ile olan bağlantımız ve projemiz, Python kodları için ana dosya olan server.py dosyası üzerinde yapılmıştır.

   Aşağıda verilen Python kodları projemizi veritabanına bağlar.

   .. code-block:: python

         def get_elephantsql_dsn(vcap_services):
          """Returns the data source name for ElephantSQL."""
          parsed = json.loads(vcap_services)
          uri = parsed["elephantsql"][0]["credentials"]["uri"]
          match = re.match('postgres://(.*?):(.*?)@(.*?)(:(\d+))?/(.*)', uri)
          user, password, host, _, port, dbname = match.groups()
          dsn = """user='{}' password='{}' host='{}' port={}
                   dbname='{}'""".format(user, password, host, port, dbname)
          return dsn

    .. code-block:: python

            if __name__ == '__main__':
                VCAP_APP_PORT = os.getenv('VCAP_APP_PORT')
                if VCAP_APP_PORT is not None:
                    port, debug = int(VCAP_APP_PORT), False
                else:
                    port, debug = 5001, True

                VCAP_SERVICES = os.getenv('VCAP_SERVICES')
                if VCAP_SERVICES is not None:
                    app.config['dsn'] = get_elephantsql_dsn(VCAP_SERVICES)
                else:
                    app.config['dsn'] = """user='vagrant' password='vagrant'
                                           host='localhost' port=1234 dbname='itucsdb'"""

                app.run(host='0.0.0.0', port=port, debug=debug)


.. toctree::

   BurakSimsek
   ZihnicanBegburs
   HilalGulsen
   ZeynepAnkara
