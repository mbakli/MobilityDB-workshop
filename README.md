# MobilityDB Workshop


Every module in this workshop illustrates a usage scenario of MobilityDB. The data sets and the tools are described inside each
of the modules.

## Documentation

You can generate the workshop documentation from the sources. Go to `/doc` directory and run: 
*  In HTML format
    ```bash
    xsltproc --stringparam html.stylesheet "docbook.css" --xinclude -o index.html /usr/share/xml/docbook/stylesheet/docbook-xsl/html/chunk.xsl mobilitydb-workshop.xml
    ```
*  In PDF format
    ```bash
    dblatex -s texstyle.sty -T native -t pdf -o mobilitydb-workshop.pdf mobilitydb-workshop.xml 
    ```
* In EPUB format
    ```bash
    dbtoepub -o mobilitydb-workshop.epub mobilitydb-workshop.xml
    ```
In addition, pre-generated versions of them are available.

*  In HTML format: https://docs.mobilitydb.com/MobilityDB-workshop/master/
*  In PDF format: https://docs.mobilitydb.com/MobilityDB-workshop/master/mobilitydb-workshop.pdf
*  In EPUB format: https://docs.mobilitydb.com/MobilityDB-workshop/master/mobilitydb-workshop.epub

## How the Repo is Organized
- `/data`: raw data files used for some workshops
- `/doc`: files needed to generate the workshop documentation from sources

## Docker container

The workshop dependencies and data files are available in a Docker container running PostgreSQL-15, PostGIS-3.4 and MobilityDB-develop (version 1.1).

*  Pull the prebuilt image from the [Docker Hub Registry](https://hub.docker.com/r/mobilitydb/mobilitydb).

    ```bash
    docker pull mobilitydb/mobilitydb:15-3.4-develop
    ```

*  Create a Docker volume to preserve the PostgreSQL database files outside of the container.
    ```bash
    docker volume create mobilitydb_data
    ```
 *  Run the Docker container.
    ```bash
    docker run --name "mobilitydb" -d -p 5432 -v mobilitydb_data:/var/lib/postgresql mobilitydb/mobilitydb:12-2.5-develop-workshop 
    ```
 *  Enter into the Docker container.
    ```bash
    docker exec -it mobilitydb bash
    ```
 *  Connect to the database  (username=docker, db=mobilitydb).
    ```bash
    psql -U docker -d mobilitydb 
    ```
 *  The workshop data files are available in the workshop directory inside the container.


## License

This workshop is licensed under a [Creative Commons Attribution-Share Alike 3.0 License](https://creativecommons.org/licenses/by-sa/3.0/)
