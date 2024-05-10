# DATABASE DESIGN

Design and schema for frog-blossom DB

• [DB schema editor](https://dbdiagram.io/d/Frog-Blossom-CMS-6631d2725b24a634d039d318)

## 6. Data Model

### 6.1 Users

- `id: bigint (primary key)`: Auto-incrementing unique ID.
- `username: varchar(255) (required)`: The username of the user.
- `email: varchar(255) (required)`: The email address of the user.
- `password: varchar(255) (required)`: The hashed password of the user.
- `role: varchar(255) (default: 'user')`: The role of the user (e.g., 'admin', 'user').
- `first_name: varchar(255)`: The first name of the user.
- `last_name: varchar(255)`: The last name of the user.
- `user_url: text`: Link to the user's personal website, blog, portfolio, or social media profile.
- `bio: text`: Biography or profile description of the user.
- `created_at: timestamptz`: Timestamp indicating when the user account was created.
- `updated_at: timestamptz`: Timestamp indicating when the user account was last updated.

### 6.2 Pages

- `id: bigserial (primary key)`: Auto-incrementing unique ID.
- `domain: varchar(255) (not null)`: The domain associated with the page.
- `page_author: bigint (not null, foreign key)`: Foreign key referencing the ID of the user who authored the page.
- `title: varchar(255) (not null)`: The title of the page.
- `url: varchar(255) (not null)`: The URL of the page.
- `menu_order: bigint (not null)`: The display order of the page in menus.
- `component_type: varchar(255) (not null)`: Type of component used in the page (e.g., 'Form', 'Text', 'Image').
- `component_value: text (not null)`: The actual data corresponding to the component type.
- `label: varchar(255) (not null)`: The label or identifier for the page.
- `option_id: bigint (not null)`: Identifier for specific settings or configurations related to the page.
- `option_name: varchar(255)`: Identifiers for specific settings or configurations (e.g., "site_title", "posts_per_page").
- `option_value: text`: Actual data or configuration settings corresponding to the option name.
- `required: boolean (not null)`: Indicates whether an option should be loaded automatically.

### 6.3 Posts

- `id: bigserial (primary key)`: Auto-incrementing unique ID.
- `title: varchar(255) (not null)`: The title of the post.
- `content: text (not null)`: The content of the post.
- `author: varchar(255) (not null)`: The author of the post.
- `created_at: timestamp (not null)`: Timestamp indicating when the post was created.
- `updated_at: timestamp`: Timestamp indicating when the post was last updated.
- `status: varchar(255) (not null)`: The status of the post (e.g., 'draft', 'pending', 'private', 'publish').
- `published_at: timestamp`: Timestamp indicating when the post was published.
- `edited_at: timestamp`: Timestamp indicating when the post was last edited.
- `post_author: bigint (foreign key)`: Foreign key referencing the ID of the user who authored the post.
- `post_mime_type: varchar(255)`: MIME type of the uploaded file for attachments.

### 6.4 Meta

- `id: bigserial (primary key)`: Auto-incrementing unique ID.
- `page_id: bigint (foreign key)`: Foreign key referencing the ID of the associated page.
- `posts_id: bigint (foreign key)`: Foreign key referencing the ID of the associated post.
- `meta_title: varchar(255)`: Title metadata associated with the post or page.
- `meta_description: text`: Description metadata associated with the post or page.
- `meta_robots: varchar(255)`: Robots metadata associated with the post or page.
- `meta_viewport: varchar(255)`: Viewport metadata associated with the post or page.
- `meta_charset: varchar(255)`: Charset metadata associated with the post or page.
- `page_amount: bigint`: Amount metadata associated with the post or page.
- `site_language: varchar(255)`: Language metadata associated with the site.
- `meta_key: varchar(255)`: Identifying key for a piece of metadata associated with a post, page, or other content types (e.g., "_thumbnail_id").
- `meta_value: varchar(255) (not null)`: The actual value of the metadata.

### 6.4 Databse diagram

![frog-blossom-db-schema-diagram](/design-docs/Frog%20Blossom%20CMS.png)

#### DBML

```sql
Table websites {
  id bigserial [primary key, unique, not null] // Auto-incrementing unique ID
  name varchar(255) [not null]
  domain varchar(255) [not null]
  owner_id bigserial [not null, ref: > users.id]
  password varchar(255)
  template_id bigserial [ref: > template.id]
  builder_enabled boolean [default: false]

  Indexes {
    owner_id
    name
    domain
  }
}

Table template {
  id bigserial [primary key, unique, not null]
  name varchar(255) [not null]

  Indexes {
    name
  }
}


Table pages {
  id bigserial [primary key, unique, not null] // Auto-incrementing unique ID
  website_id bigserial [not null, ref: > websites.id]
  title varchar(255) [not null]
  content text [not null]
  url varchar(255) [not null]

  Indexes {
    website_id
    title
  }
}

Table site_meta_tags {
  id bigserial [primary key, unique, not null] // Auto-incrementing unique ID
  page_id bigserial [not null, ref: > pages.id]
  name varchar(255) [not null]
  content text [not null]

  Indexes {
    page_id
    name
  }
}

Table contact_forms {
  id bigserial [primary key, unique, not null] // Auto-incrementing unique ID
  website_id bigserial [not null, ref: > websites.id]
  form_id varchar(255) [not null]
}

Table form_fields {
  id bigserial [primary key, unique, not null] // Auto-incrementing unique ID
  form_id bigserial [not null, ref: > contact_forms.id]
  label varchar(255) [not null]
  type varchar(255) [not null]
  required boolean [not null]
}

Table template_list {
  id bigserial [primary key, unique, not null] // Auto-incrementing unique ID
  name varchar(255) [not null]
  preview_image_url varchar(255) [not null]

  Indexes {
    name
  }
}

Table layout_options {
  id bigserial [primary key, unique, not null] // Auto-incrementing unique ID
  name varchar(255) [not null]
  description text [not null]
  preview_image_url varchar(255) [not null]
}

Table users {
  id bigserial [primary key, unique, not null] // Auto-incrementing unique ID
  username varchar(255) [not null, unique]
  email varchar(255) [not null, unique]
  password varchar(255) [not null]
  role varchar(255) [default: 'user']
  owner_id bigserial [not null, ref: > websites.id]
  first_name varchar(255)
  last_name varchar(255)
  avatar_url varchar(255)
  bio text
  created_at timestamptz [default: `now()`]
  updated_at timestamptz

  Indexes {
    username
    owner_id
  }
}


Table content {
  id bigserial [primary key, unique, not null] // Auto-incrementing unique ID
  title varchar(255) [not null]
  body text [not null]
  author_id bigserial [not null, ref: > users.id]
  created_at timestamp [default: `now()`, not null]
  updated_at timestamp
  status varchar(255) [not null]
  published_at timestamp
  edited_at timestamp
  organization_id bigserial [ref: > organizations.id]
  published_by_id bigserial [ref: > users.id]

  Indexes {
    author_id
    created_at
    updated_at
    organization_id
    title
    (created_at, updated_at)
  }
}

Table organizations {
  id bigserial [primary key, unique, not null]
  name varchar(255) [not null]
}

Table content_meta_tags {
  id bigserial [primary key, unique, not null] // Auto-incrementing unique ID
  content_id bigserial [ref: > content.id]
  name varchar(255) [not null]
  content text [not null]

  Indexes {
    content_id
  }
}

Table content_categories {
  id bigserial [primary key, unique, not null] // Auto-incrementing unique ID
  content_id bigserial [ref: > content.id]
  category_id bigserial [ref: > categories.id]
}

Table categories {
  id bigserial [primary key, unique, not null] // Auto-incrementing unique ID
  name varchar(255) [not null]

  Indexes {
    name
  }
}
```

frog-blossom-db schema v.2

```sql
Table users {
  id bigserial [primary key, unique, not null]
  username varchar(255) [not null, unique]
  email varchar(255) [not null, unique]
  password varchar(255) [not null]
  role varchar(255) [default: 'user']
  first_name varchar(255)
  last_name varchar(255)
  avatar_url varchar(255)
  bio text
  created_at timestamptz [default: `now()`]
  updated_at timestamptz

  Indexes {
    username
  }
}

Table website {
  id bigserial [primary key, unique, not null]
  name varchar(255) [not null]
  domain varchar(255) [not null]
  owner_id int [not null, ref: > users.id]
  selected_template int [ref: > template.id]

  Indexes {
    owner_id
    name
    domain
  }
}

Table template {
  id bigserial [primary key, unique, not null]
  name varchar(255) [not null]

  Indexes {
    name
  }
}

Ref: website_template.(website_id, template_id) > website.(id, selected_template)

Table website_template {
  website_id int [ref: > website.id]
  template_id int [ref: > template.id]
}

Table pages {
  id bigserial [primary key, unique, not null]
  website_id int [not null, ref: > website.id]
  title varchar(255) [not null]
  url varchar(255) [not null]

  Indexes {
    website_id
    title
  }
}

Table page_components {
  id bigserial [primary key, unique, not null]
  page_id int [not null, ref: > pages.id]
  component_type varchar(255) [not null] // Type of component: 'Form', 'Text', 'Image', etc.
  component_data jsonb [not null] // JSON data representing the component's content and settings

  Indexes {
    page_id
  }
}

Table content {
  id bigserial [primary key, unique, not null] // Auto-incrementing unique ID
  title varchar(255) [not null]
  body text [not null]
  author_id int [not null, ref: > users.id]
  created_at timestamp [default: `now()`, not null]
  updated_at timestamp
  status varchar(255) [not null]
  published_at timestamp
  edited_at timestamp
  published_by_id int [ref: > users.id]
  component_id int [not null, ref: > page_components.id] // Reference to the parent form component

  Indexes {
    author_id
    created_at
    updated_at
    title
    (created_at, updated_at)
  }
}

Table content_images {
  id bigserial [primary key, unique, not null] // Auto-incrementing unique ID
  content_id int [ref: > content.id]
  file_path varchar(255) [not null]
  title varchar(255) [not null]
  description varchar(255) [not null]
  alt_text VARCHAR(255)
}

Table form_fields {
  id bigserial [primary key, unique, not null]
  component_id int [not null, ref: > page_components.id] // Reference to the parent form component
  label varchar(255) [not null]
  type varchar(255) [not null] // Field type: 'Text', 'Textarea', 'Email', 'Checkbox', etc.
  required boolean [not null]
}
```

frog-blossom-db schema v.3

```sql

Table users {
  id bigserial [primary key, unique, not null]
  username varchar(255) [not null]
  email varchar(255) [not null]
  password varchar(255) [not null]
  role varchar(255) [default: 'user']
  first_name varchar(255)
  last_name varchar(255)
  avatar_url varchar(255)
  bio text
  created_at timestamptz [default: `now()`]
  updated_at timestamptz

  Indexes {
    username
  }
}

Table website {
  id bigserial [primary key, unique, not null]
  name varchar(255) [not null]
  domain varchar(255) [not null]
  owner_id bigint [not null, ref: > users.id]

  Indexes {
    owner_id
    name
    domain
  }
}

Table pages {
  id bigserial [primary key, unique, not null]
  website_id bigint [not null, ref: > website.id]
  title varchar(255) [not null]
  url varchar(255) [not null]
  menu_order bigint [not null] // holds the display number for pages and other non-post types.
}

Table page_components {
  id bigserial [primary key, unique, not null]
  page_id bigint [not null, ref: > pages.id]
  component_type varchar(255) [not null] // Type of component: 'Form', 'Text', 'Image','Email', 'Checkbox', etc.
  component_value text [not null] // actual data of the corresponding to type
  label varchar(255) [not null]
  option_id bigint [not null]
  option_name varchar(255) // identifiers for specific settings or configurations: "site_title" "posts_per_page"
  option_value text // actual data or configuration settings corresponding to the option name
  required boolean [not null] // indicates whether an option should be loaded automatically
}

Table posts {
  id bigserial [primary key, unique, not null] // Auto-incrementing unique ID
  title varchar(255) [not null]
  content text [not null]
  author varchar(255) [not null]
  created_at timestamp [default: `now()`, not null]
  updated_at timestamp
  status varchar(255) [not null] // ‘draft’, ‘pending’, ‘private’, ‘publish’
  published_at timestamp
  edited_at timestamp
  published_by_id bigint [ref: > users.id]
  website_id bigint [ref: > website.id]
  post_mime_type varchar(255) // for attachments, the MIME type of the uploaded file: "image/jpeg" "application/pdf"

  Indexes {
    created_at
    updated_at
    title
    (created_at, updated_at)
  }
}

Table meta {
  id bigserial [primary key, unique, not null]
  page_id bigint [ref: > pages.id] // Foreign key referencing the page table
  posts_id bigint [ref: > posts.id] // Foreign key referencing the posts table
  meta_title varchar(255)
  meta_description text
  meta_robots varchar(255)
  meta_viewport varchar(255)
  meta_charset varchar(255)
  website_id bigint [not null, ref: > website.id]
  page_amount bigint
  site_language varchar(255)
  meta_key varchar(255) // identifying key for a piece of metadata associated with a post, page, or other content types: "_thumbnail_id"
  meta_value varchar(255) [not null]  
}

```

frog-blossom-db schema v.4

```sql
Table users {
  id bigserial [primary key, unique, not null]
  username varchar(255) [not null]
  email varchar(255) [not null]
  password varchar(255) [not null]
  role varchar(255) [default: 'user']
  first_name varchar(255)
  last_name varchar(255)
  user_url text [null] //  link to user personal website, blog, portfolio, social media profile
  bio text
  created_at timestamptz [default: `now()`]
  updated_at timestamptz

  Indexes {
    username
    first_name
    last_name
    (created_at, updated_at)
  }
}

Table pages {
  id bigserial [primary key, unique, not null]
  domain varchar(255) [not null]
  page_author bigint [not null, ref: > users.id]
  title varchar(255) [not null]
  url varchar(255) [not null]
  menu_order bigint [not null] // holds the display number for pages and other non-post types.
  component_type varchar(255) [not null] // Type of component: 'Form', 'Text', 'Image','Email', 'Checkbox', etc.
  component_value text [not null] // actual data of the corresponding to type
  label varchar(255) [not null]
  option_id bigint [not null]
  option_name varchar(255) // identifiers for specific settings or configurations: "site_title" "posts_per_page"
  option_value text // actual data or configuration settings corresponding to the option name
  required boolean [not null] // indicates whether an option should be loaded automatically

  Indexes {
    page_author
    domain
    url
  }
}

Table posts {
  id bigserial [primary key, unique, not null] // Auto-incrementing unique ID
  title varchar(255) [not null]
  content text [not null]
  author varchar(255) [not null]
  created_at timestamp [default: `now()`, not null]
  updated_at timestamp
  status varchar(255) [not null] // ‘draft’, ‘pending’, ‘private’, ‘publish’
  published_at timestamp
  edited_at timestamp
  post_author bigint [ref: > users.id]
  post_mime_type varchar(255) // for attachments, the MIME type of the uploaded file: "image/jpeg" "application/pdf"

  Indexes {
    created_at
    updated_at
    title
    (created_at, updated_at)
  }
}

Table meta {
  id bigserial [primary key, unique, not null]
  page_id bigint [ref: > pages.id] // Foreign key referencing the page table
  posts_id bigint [ref: > posts.id] // Foreign key referencing the posts table
  meta_title varchar(255)
  meta_description text
  meta_robots varchar(255)
  meta_viewport varchar(255)
  meta_charset varchar(255)
  page_amount bigint
  site_language varchar(255)
  meta_key varchar(255) // identifying key for a piece of metadata associated with a post, page, or other content types: "_thumbnail_id"
  meta_value varchar(255) [not null]
}

```

### Revision History

| Date       | Version | Description of Changes              | Author |
|------------|---------|------------------------------------|--------|
| 2024-04-26 | 1.0     | Initial draft of document          | @minierparedes    |
| 2024-04-30 | 1.1     | Creat C4 Model Diagrams            | @minierparedes    |
| 2024-05-02 | 1.2     |scenario walkthough | @minierparedes    |
| 2024-05-08 | 1.2     |per discussion [slack](https://reflectionizm.slack.com/archives/D06FJ2S89FC/p1715159910604659) | @minierparedes    |
| 2024-05-10 | 1.2     |frog-blossom-db schema v.4 | @minierparedes    |
