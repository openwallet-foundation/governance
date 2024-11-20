This repository controls the teams and repositories that are part of the
OpenWallet Foundation organization on GitHub ([openwallet-foundation]).
Specifically, this repository utilizes [CloWarden] to manage the teams and
repositories.

The following GitHub actions are supported by modifying the `config.yaml` file
in this repository:

- Add teams
- Remove teams
- Add maintainers or members to teams
- Remove maintainers or members from teams
- Add repositories
- Add teams to repositories
- Remove teams from repositories
- Update teams' role in repository
- Add collaborators to repositories
- Remove collaborators from repositories
- Update collaborators' role in repository
- Update repository visibility

This repository can be modified by any maintainer of any OpenWallet Foundation
Growth or Impact projects. In general, we expect that there will be a set of
teams for each project:

| Team Name | Description | [Typical Permissions] |
| --------- | ----------- | ------------------- |
| _project_-admins | Administrators for a given project | Admin |
| _project_-committers | Committers for a given project | Maintain |
| _project_-contributors | Contributors for a given project | Triage |

Optionally, there may be a set of teams for each repository within a project:

| Team Name | Description | [Typical Permissions] |
| --------- | ----------- | ------------------- |
| _repo_-admins | Administrators for a given repository | Admin |
| _repo_-committers | Committers for a given repository | Maintain |
| _repo_-contributors | Contributors for a given repository | Triage |

**NOTES**:

1. Per repository teams are not needed if a project has only one repository, or if all the same people control all of the repositories within the project.
2. Each repository **SHOULD** have either or both of the project and repository teams included on each repository.

## GitHub Permissions
The permissions that can be provided to different teams are:

- **Read**: Recommended for non-code contributors who want to view or discuss your project (not needed since all repositories within OpenWallet Foundation should have public visibility).
- **Triage**: Recommended for contributors who need to proactively manage issues, discussions, and pull requests without write access.
- **Write**: Recommended for contributors who actively push to your project.
- **Maintain**: Recommended for project managers who need to manage the repository without access to sensitive or destructive actions.
- **Admin**: Recommended for people who need full access to the project, including sensitive and destructive actions like managing security or deleting a repository.

## Some tips to avoid problems

It's important to keep in mind that..

- GitHub usernames are case sensitive
- Repositories and team names must contain only lowercase letters, numbers or hyphens (in the case of teams, the GitHub team slug must be used)
- Teams maintainers must belong to the organization before being added to the teams
- Teams maintainers and members fields can be omitted when the field formation is defined and one of the subteams has at least one maintainer
- It is possible to use the formation field in teams and at the same time explicitly define some team maintainers and members
- Teams formation is not recursive. If a subteam is also using formation, its subteams will be ignored
- GitHub repositories permissions granted using teams won't be effective until the team member has accepted the invitation to the organization
- Before renaming a GitHub username, make sure it's not used as a team maintainer in the configuration file

## config.yaml Format

```
teams:
  - name: <github_team_slug>
    # Team maintainers
    #
    #   - Values must be valid GitHub usernames (case sensitive)
    #   - At least one team maintainer must be specified
    #   - Maintainers must already be members of the organization
    maintainers:
      - <github_username>
      - <github_username>

    # Team members
    #
    #   - Values must be valid GitHub usernames (case sensitive)
    members:
      - <github_username>
      - <github_username>

repositories:
  - name: <github_repository_name>
    # Teams with access to the repository.
    # See https://docs.github.com/en/organizations/managing-user-access-to-your-organizations-repositories/managing-repository-roles/repository-roles-for-an-organization
    #
    #   - Key: GitHub team slug
    #   - Value: access level
    #   - Value options: read | triage | write | maintain | admin
    teams:
      <project>-admins: admin
      <project>-committers: maintain
      <project>-contributors: triage
      <repo>-admins: admin
      <repo>-committers: maintain
      <repo>-contributors: triage

    # Repository visibility
    #
    #   - Value options: public | private | internal
    #   - Default: public
    #   - All repositories within OpenWallet Foundation should have public visibility
    visibility: public
```

## References

* [CloWarden]
* [GitHub Permissions]

[openwallet-foundation]: https://github.com/openwallet-foundation
[CloWarden]: https://github.com/cncf/clowarden
[Typical Permissions]: https://docs.github.com/en/enterprise-cloud@latest/organizations/managing-user-access-to-your-organizations-repositories/managing-repository-roles/repository-roles-for-an-organization#permissions-for-each-role
[GitHub Permissions]: https://docs.github.com/en/organizations/managing-user-access-to-your-organizations-repositories/managing-repository-roles/repository-roles-for-an-organization

