---
title: Uniform Resource Ingest Session PLM Account Project
---

## Description

Immutable ingest session folder system represents an organisation issues to be ingested. Each  session includes an organisation, then name is the  folder that was scanned.

<details>
<summary><strong>Table Definition</strong></summary>

```sql
CREATE TABLE "ur_ingest_session_plm_acct_project" (
    "ur_ingest_session_plm_acct_project_id" VARCHAR PRIMARY KEY NOT NULL,
    "ingest_session_id" VARCHAR NOT NULL,
    "ingest_account_id" VARCHAR NOT NULL,
    "parent_project_id" TEXT,
    "name" TEXT NOT NULL,
    "description" TEXT,
    "id" TEXT,
    "key" TEXT,
    "elaboration" TEXT CHECK(json_valid(elaboration) OR elaboration IS NULL),
    "created_at" TIMESTAMPTZ DEFAULT CURRENT_TIMESTAMP,
    "created_by" TEXT DEFAULT 'UNKNOWN',
    "updated_at" TIMESTAMPTZ,
    "updated_by" TEXT,
    "deleted_at" TIMESTAMPTZ,
    "deleted_by" TEXT,
    "activity_log" TEXT,
    FOREIGN KEY("ingest_session_id") REFERENCES "ur_ingest_session"("ur_ingest_session_id"),
    FOREIGN KEY("ingest_account_id") REFERENCES "ur_ingest_session_plm_account"("ur_ingest_session_plm_account_id"),
    UNIQUE("name", "description")
)
```

</details>

## Columns

| Name                                  | Type        | Default           | Nullable | Children                                                                                                                                                                                                                                                                                                                                                            | Parents                                                           | Comment                                                 |
| ------------------------------------- | ----------- | ----------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- | ------------------------------------------------------- |
| ur_ingest_session_plm_acct_project_id | VARCHAR     |                   | false    | [uniform_resource](/docs/standard-library/rssd-schema/uniform_resource) [ur_ingest_session_plm_acct_project_issue](/docs/standard-library/rssd-schema/ur_ingest_session_plm_acct_project_issue) [ur_ingest_session_plm_acct_label](/docs/standard-library/rssd-schema/ur_ingest_session_plm_acct_label) [ur_ingest_session_plm_milestone](/docs/standard-library/rssd-schema/ur_ingest_session_plm_milestone) [ur_ingest_session_plm_acct_relationship](/docs/standard-library/rssd-schema/ur_ingest_session_plm_acct_relationship) |                                                                   | {"isSqlDomainZodDescrMeta":true,"isVarChar":true}       |
| ingest_session_id                     | VARCHAR     |                   | false    |                                                                                                                                                                                                                                                                                                                                                                     | [ur_ingest_session](/docs/standard-library/rssd-schema/ur_ingest_session)                         | {"isSqlDomainZodDescrMeta":true,"isVarChar":true}       |
| ingest_account_id                     | VARCHAR     |                   | false    |                                                                                                                                                                                                                                                                                                                                                                     | [ur_ingest_session_plm_account](/docs/standard-library/rssd-schema/ur_ingest_session_plm_account) | {"isSqlDomainZodDescrMeta":true,"isVarChar":true}       |
| parent_project_id                     | TEXT        |                   | true     |                                                                                                                                                                                                                                                                                                                                                                     |                                                                   | References itself to allow subprojects.                 |
| name                                  | TEXT        |                   | false    |                                                                                                                                                                                                                                                                                                                                                                     |                                                                   | The name of the project                                 |
| description                           | TEXT        |                   | true     |                                                                                                                                                                                                                                                                                                                                                                     |                                                                   |                                                         |
| id                                    | TEXT        |                   | true     |                                                                                                                                                                                                                                                                                                                                                                     |                                                                   |                                                         |
| key                                   | TEXT        |                   | true     |                                                                                                                                                                                                                                                                                                                                                                     |                                                                   |                                                         |
| elaboration                           | TEXT        |                   | true     |                                                                                                                                                                                                                                                                                                                                                                     |                                                                   | {"isSqlDomainZodDescrMeta":true,"isJsonText":true}      |
| created_at                            | TIMESTAMPTZ | CURRENT_TIMESTAMP | true     |                                                                                                                                                                                                                                                                                                                                                                     |                                                                   |                                                         |
| created_by                            | TEXT        | 'UNKNOWN'         | true     |                                                                                                                                                                                                                                                                                                                                                                     |                                                                   |                                                         |
| updated_at                            | TIMESTAMPTZ |                   | true     |                                                                                                                                                                                                                                                                                                                                                                     |                                                                   |                                                         |
| updated_by                            | TEXT        |                   | true     |                                                                                                                                                                                                                                                                                                                                                                     |                                                                   |                                                         |
| deleted_at                            | TIMESTAMPTZ |                   | true     |                                                                                                                                                                                                                                                                                                                                                                     |                                                                   |                                                         |
| deleted_by                            | TEXT        |                   | true     |                                                                                                                                                                                                                                                                                                                                                                     |                                                                   |                                                         |
| activity_log                          | TEXT        |                   | true     |                                                                                                                                                                                                                                                                                                                                                                     |                                                                   | {"isSqlDomainZodDescrMeta":true,"isJsonSqlDomain":true} |

## Constraints

| Name                                                  | Type        | Definition                                                                                                                                                     |
| ----------------------------------------------------- | ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ur_ingest_session_plm_acct_project_id                 | PRIMARY KEY | PRIMARY KEY (ur_ingest_session_plm_acct_project_id)                                                                                                            |
| - (Foreign key ID: 0)                                 | FOREIGN KEY | FOREIGN KEY (ingest_account_id) REFERENCES ur_ingest_session_plm_account (ur_ingest_session_plm_account_id) ON UPDATE NO ACTION ON DELETE NO ACTION MATCH NONE |
| - (Foreign key ID: 1)                                 | FOREIGN KEY | FOREIGN KEY (ingest_session_id) REFERENCES ur_ingest_session (ur_ingest_session_id) ON UPDATE NO ACTION ON DELETE NO ACTION MATCH NONE                         |
| sqlite_autoindex_ur_ingest_session_plm_acct_project_2 | UNIQUE      | UNIQUE (name, description)                                                                                                                                     |
| sqlite_autoindex_ur_ingest_session_plm_acct_project_1 | PRIMARY KEY | PRIMARY KEY (ur_ingest_session_plm_acct_project_id)                                                                                                            |
| -                                                     | CHECK       | CHECK(json_valid(elaboration) OR elaboration IS NULL)                                                                                                          |

## Indexes

| Name                                                      | Definition                                                                                                                              |
| --------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| idx_ur_ingest_session_plm_acct_project__name__description | CREATE INDEX "idx_ur_ingest_session_plm_acct_project__name__description" ON "ur_ingest_session_plm_acct_project"("name", "description") |
| sqlite_autoindex_ur_ingest_session_plm_acct_project_2     | UNIQUE (name, description)                                                                                                              |
| sqlite_autoindex_ur_ingest_session_plm_acct_project_1     | PRIMARY KEY (ur_ingest_session_plm_acct_project_id)                                                                                     |

## Relations

![er](../../../../../assets/images/content/docs/standard-library/rssd-schema/ur_ingest_session_plm_acct_project.svg)
