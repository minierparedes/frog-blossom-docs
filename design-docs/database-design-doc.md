# DATABASE DESIGN

Design and schema for frog-blossom DB

• [DB schema editor](https://dbdiagram.io/d/Frog-Blossom-CMS-6631d2725b24a634d039d318)



## 6. Data Model

### 6.1 Website

- `name: String (required)`: The name or title of the website.
- `domain: String (required)`: The domain name or URL of the website.
- `owner_id: String (required)`: The ID of the user who owns or manages the website.
- `password: String`: A hashed password for accessing the website's administrative features (optional).
- `template_id: String`: The ID of the theme applied to the website (optional).
- `pages: Array`: An array of page objects representing the pages within the website.
  - `page_id: String`: The unique identifier for the page.
  - `title: String`: The title of the page.
  - `content: String`: The content or body of the page.
  - `url: String`: The URL or path of the page within the website.
  - `site_meta_tags: Array`: An array of meta tag objects associated with the page.
    - `name: String`: The name of the meta tag.
    - `content: String`: The content of the meta tag.
- `builder_enabled: Boolean`: Indicates whether the website builder is enabled for this website.
- `contact_forms: Array`: An array of contact form objects available on the website.
  - `form_id: String`: The unique identifier for the contact form.
  - `fields: Array`: An array of form field objects defining the fields in the contact form.
    - `field_id: String`: The unique identifier for the form field.
    - `label: String`: The label or name of the form field.
    - `type: String`: The type of the form field (e.g., text, email, textarea, checkbox, etc.).
    - `required: Boolean`: Indicates whether the form field is required.
- `templates: Array`: An array of template objects available for the website.
  - `template_id: String`: The unique identifier for the template.
  - `name: String`: The name or title of the template.
  - `preview_image_url: String`: The URL of a preview image for the template.
- `layout_options: Array`: An array of flexible layout options available for the website.
  - `layout_id: String`: The unique identifier for the layout option.
  - `name: String`: The name or title of the layout option.
  - `description: String`: A brief description of the layout option.
  - `preview_image_url: String`: The URL of a preview image for the layout option.


### 6.2 User

- `username: String (required)`: The unique username of the user.
- `email: String (required)`: The email address of the user.
- `password: String (required, hashed)`: The hashed password of the user.
- `role: String (default: "user" or "admin")`: The role of the user, determining their permissions and access levels.
- `first_name: String`: The first name of the user.
- `last_name: String`: The last name of the user.
- `avatar_url: String`: The URL of the user's avatar or profile picture.
- `bio: String`: A short biography or description of the user.
- `created_at: Date (default: current timestamp)`: The date and time when the user account was created.
- `updated_at: Date`: The date and time when the user account was last updated.


### 6.3 Content

- `title: String (required)`: The title of the content.
- `content: String (required)`: The body or main content of the article.
- `author: ObjectId (referring to User)`: The ID of the user who authored the content.
- `createdAt: Date (default: current timestamp)`: The date and time when the content was created.
- `updatedAt: Date`: The date and time when the content was last updated.
- `content_meta_tags: Array`: An array of meta tag objects associated with the content.
  - `name: String`: The name of the meta tag.
  - `content: String`: The content of the meta tag.
- `categories: Array`: An array of category IDs or objects to which the content belongs.
- `status: String`: The status of the content (e.g., draft, published, archived, etc.).
- `publishedAt: Date`: The date and time when the content was published (if applicable).
- `editedAt: Date`: The date and time when the content was last edited.
- `organization_id: ObjectId`: The ID of the organization to which the content belongs (if applicable).
- `publishedBy: ObjectId (referring to User)`: The ID of the user who published the content (if applicable).


### 6.4 Databse diagram

![frog-blossom-db-schema-diagram](/design-docs/Frog%20Blossom%20CMS.png)

### 6.5 Table & relationships 

```sql
Ref: users.owner_id > websites.id
Ref: users.id < content.author_id
Ref: users.id < content.published_by_id
Ref: websites.id < pages.website_id
Ref: pages.id < site_meta_tags.page_id
Ref: websites.id < contact_forms.website_id
Ref: contact_forms.id < form_fields.form_id
Ref: content.id < content_meta_tags.content_id
Ref: content.id < content_categories.content_id
Ref: categories.id < content_categories.category_id
```

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
