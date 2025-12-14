# Lab 2 — Gestion de stock (Sortie) : Dictionnaire, Règles, MCD, MLD
# MCD
![URL](https://github.com/fe045001-netizen/Tp2Merise/blob/1fb5cb253bb88f60b069ba04a9a049e102bf5efe/MCD.png)
 # MLD:
![URL](https://github.com/fe045001-netizen/Tp2Merise/blob/1fb5cb253bb88f60b069ba04a9a049e102bf5efe/MPD.png)

```sql
/*==============================================================*/
/* Nom de SGBD :  MySQL 4.0                                     */
/* Date de création :  14/12/2025 21:44:53                      */
/*==============================================================*/


drop index PASSER_FK on COMMANDE;

drop index CONCERNER2_FK on CONCERNER;

drop index CONCERNER_FK on CONCERNER;

drop table if exists CLIENT;

drop table if exists COMMANDE;

drop table if exists CONCERNER;

drop table if exists PRODUIT;

/*==============================================================*/
/* Table : CLIENT                                               */
/*==============================================================*/
create table CLIENT
(
   IDCLIENT                       int                            not null,
   NOMCLIENT                      text                           not null,
   PRENOMCLIENT                   text                           not null,
   ADRESSECLIENT                  text                           not null,
   primary key (IDCLIENT)
)
type = InnoDB;

/*==============================================================*/
/* Table : COMMANDE                                             */
/*==============================================================*/
create table COMMANDE
(
   NOMCMD                         int                            not null,
   IDCLIENT                       int                            not null,
   DATECMD                        date                           not null,
   ADRESSELIV                     text                           not null,
   primary key (NOMCMD)
)
type = InnoDB;

/*==============================================================*/
/* Index : PASSER_FK                                            */
/*==============================================================*/
create index PASSER_FK on COMMANDE
(
   IDCLIENT
);

/*==============================================================*/
/* Table : CONCERNER                                            */
/*==============================================================*/
create table CONCERNER
(
   CODEPROD                       text                           not null,
   NOMCMD                         int                            not null,
   QTECMD                         int                            not null,
   primary key (CODEPROD, NOMCMD)
)
type = InnoDB;

/*==============================================================*/
/* Index : CONCERNER_FK                                         */
/*==============================================================*/
create index CONCERNER_FK on CONCERNER
(
   CODEPROD
);

/*==============================================================*/
/* Index : CONCERNER2_FK                                        */
/*==============================================================*/
create index CONCERNER2_FK on CONCERNER
(
   NOMCMD
);

/*==============================================================*/
/* Table : PRODUIT                                              */
/*==============================================================*/
create table PRODUIT
(
   CODEPROD                       text                           not null,
   LIBPROD                        text,
   PRIXUNIT                       decimal,
   primary key (CODEPROD)
)
type = InnoDB;

alter table COMMANDE add constraint FK_PASSER foreign key (IDCLIENT)
      references CLIENT (IDCLIENT) on delete restrict on update restrict;

alter table CONCERNER add constraint FK_CONCERNER foreign key (CODEPROD)
      references PRODUIT (CODEPROD) on delete restrict on update restrict;

alter table CONCERNER add constraint FK_CONCERNER2 foreign key (NOMCMD)
      references COMMANDE (NOMCMD) on delete restrict on update restrict;

```

