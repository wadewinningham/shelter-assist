# Shelter Assist

Be sure to edit this file as things change…

## Current mental model and direction of development:

A Rescue is an organization made up of People who are
Volunteers and/or Fosters.

Anyone caring for an Animal is a Foster.
Fosters must have a Home. Animals must have a Home.

An Animal will move from one Home to another and that may change their Foster.

That means that members of an organization who are administrators, are Fosters. They may have a shelter where an animal is housed, which is the animal's Home. Or those administrators may be housing an animal at their actual house, which will still be the animal's Home.

Members of an organization who volunteer to help with transporting animals from one place to another, would also be a Foster. And whatever locations are used for transporting _to_ and _from_ should be recorded as Homes with a Foster associated to each one.

People outside of the organization can signup to become a Foster where the system should record their information and create:

  1. their Foster record
  2. their Home record
  3. their Application to become a Foster.

When an Adoption event occurs, the Animal may change Fosters and/or Homes but would no longer have a Need for Adoption.

### Animal Needs

The system should enable admins to manage the Needs of 1 or more Animals for a Rescue. An Animal may need to move from one Home to another quickly. Multiple animals may need to move from one Home to another by a certain date.

The system should help admins make decisions about what Fosters are available and appropriate (e.g. barring exclusions) for the Animal(s) Needs.

### Exclusions

Fosters may have Exclusions that would prevent them from being a Foster. Recording these exclusions could be automatic and/or could be manually assigned by an admin.

Homes may have Exclusions that would prevent them from housing an Animal. Recording these exclusions could be automatic and/or could be manually assigned by an admin.

### Foster Communication

Different Fosters respond to the needs of an organization differently. Some work well with SMS, others with email, still others work best with phone calls. The system should help admins or Fosters themselves manage this.

The system should provide a way to send a message about Animal Needs to a group of Fosters in the manner most appropriate to the Foster.

Each Foster should have an admin (or other role) primary point of contact with whom the Foster would have a good relationship.

### Likely to change…

Fosters currently have a boolean `admin` column. It's likely this should instead become some way of managing a "role".

Records like a Person who is a Foster and Application will likely need a way of tracking _status_ (approved, rejected, etc.).

**Multitenancy** should be added ASAP. There are currently 2 organizations looking to use this software. Data for one Rescue should not be visible to other Rescues.

## Set up

All commands in code font are to be copied and pasted onto command line.

1. `git clone https://github.com/rubyforgood/shelter-assist.git`
1. `brew install rbenv`
1. `rbenv install 3.0.2`
1. `rbenv init`   
1. `rbenv local 3.0.2`
1. Close the CLI tab and open a new one
1. `brew install yarn`
1. `cd path/to/shelter-assist`
1. `brew install postgresql` (idk, bundle didn't work until I installed this first)
1. `bundle install`
1. `yarn install`
1. `brew services restart postgresql`
1. `bin/rails db:create`
1. `bin/rails db:migrate RAILS_ENV=development`
1. `bin/dev`

## Optional ASDF-VM Support

Note: a `.tool-versions` file exists which contains the current supported ruby version

* `asdf plugin-add ruby`
* `asdf install`

## Running the app

```
rails s
```

## Design

|                          |                                                              |
| ------------------------ | ------------------------------------------------------------ |
| Design system            | [Ant Design](https://ant.design)                             |
| Components in Figma File | [Ant Design Open Source Figma Library](https://www.figma.com/community/file/831698976089873405) |
| Homepage Illustrations   | [unDraw](https://undraw.co/search) illustrations, free for commercial use. |
| Fonts Used               | _Speech Bubble Text_ - Sue Ellen Francisco<br />_Roboto_ (Regular, Bold) |

### Design Prototypes

- [Foster Application](https://www.figma.com/proto/RIfWeZXYmQJEA9Tuwxewzy/Design-File?node-id=86%3A27199&viewport=241%2C48%2C0.69&scaling=min-zoom&starting-point-node-id=86%3A27475&show-proto-sidebar=1)
- [Volunteer Sign In / Add a Pet / Pet Profile / User Profile](https://www.figma.com/proto/RIfWeZXYmQJEA9Tuwxewzy/Design-File?node-id=86%3A27199&viewport=241%2C48%2C0.69&scaling=min-zoom&starting-point-node-id=86%3A27203&show-proto-sidebar=1)

## Setting up and testing mail delivery using Mailhog in local development

The following is how to setup mailhog, which is a tool to intercept e-mails in a local environment for e-mail testing purposes. The following steps only apply to MacOS users. For non MacOS users, please refer to `https://mailtrap.io/blog/mailhog-explained/`

1.  Set up Mailhog using Homebrew. Run the following command in the terminal: 

  * `brew install mailhog`

2. Then start Mailhog in the terminal with:

  * `brew services start mailhog`

3. After sending an e-mail locally in a test environment, visit the following link: 

  * `http://localhost:8025/`

4. To stop Mailhog use:

  * `brew services stop mailhog`

## Production/Staging Setup

### Environment Variables

For the hosting environment, you'll need the following environment variables setup to point to your SMTP/Email service.

```
SHELTERASSIST_HOSTNAME = "https://shelterassist.herokuapp.com
SHELTERASSIST_SMTP_SERVER = "smtp.example.com"
SHELTERASSIST_SMTP_PORT = 587
SHELTERASSIST_SMTP_USER = "myusername"
SHELTERASSIST_SMTP_PASSWORD = "password"
SHELTERASSIST_EMAIL_ADDRESS = "support@shelterassist.org"
```

`SHELTERASSIST_EMAIL_ADDRESS` is the _from_ address used for outgoing email like password reminders and magic-link emails.
