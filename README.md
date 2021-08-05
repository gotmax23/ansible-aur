# Ansible Collection - gotmax23.aur_test
This collection is intended for testing [this PR](https://github.com/kewlfft/ansible-aur/pull/58). Please do not actually use it.
<table  border=0 cellpadding=0 class="documentation-table">
    <tr>
        <th colspan="1">Parameter</th>
        <th>Choices/<font color="blue">Defaults</font></th>
                    <th width="100%">Comments</th>
    </tr>
                <tr>
                                                            <td colspan="1">
                <div class="ansibleOptionAnchor" id="parameter-aur_only"></div>
                <b>aur_only</b>
                <a class="ansibleOptionLink" href="#parameter-aur_only" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">boolean</span>
                                                                </div>
                                                    </td>
                            <td>
                                                                                                                                                                                                                <ul style="margin: 0; padding: 0"><b>Choices:</b>
                                                                                                                                                            <li><div style="color: blue"><b>no</b>&nbsp;&larr;</div></li>
                                                                                                                                                                                            <li>yes</li>
                                                                                </ul>
                                                                        </td>
                                                            <td>
                                        <div>Limit helper operation to the AUR. Dependency resolution will still include repository packages.</div>
                                                    </td>
        </tr>
                            <tr>
                                                            <td colspan="1">
                <div class="ansibleOptionAnchor" id="parameter-extra_args"></div>
                <b>extra_args</b>
                <a class="ansibleOptionLink" href="#parameter-extra_args" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">string</span>
                                                                </div>
                                                    </td>
                            <td>
                                                                                                                                                        </td>
                                                            <td>
                                        <div>A list of additional arguments to pass directly to the AUR helper. You must explicitly set &#x27;use&#x27; to something other than &#x27;auto&#x27; to use thi soption.</div>
                                                    </td>
        </tr>
                            <tr>
                                                            <td colspan="1">
                <div class="ansibleOptionAnchor" id="parameter-ignore_arch"></div>
                <b>ignore_arch</b>
                <a class="ansibleOptionLink" href="#parameter-ignore_arch" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">boolean</span>
                                                                </div>
                                                    </td>
                            <td>
                                                                                                                                                                                                                <ul style="margin: 0; padding: 0"><b>Choices:</b>
                                                                                                                                                            <li><div style="color: blue"><b>no</b>&nbsp;&larr;</div></li>
                                                                                                                                                                                            <li>yes</li>
                                                                                </ul>
                                                                        </td>
                                                            <td>
                                        <div>Only supported with makepkg. Ignore a missing or incomplete arch field. This is useful when the PKGBUILD does not have the arch=(&#x27;yourarch&#x27;) field.</div>
                                                    </td>
        </tr>
                            <tr>
                                                            <td colspan="1">
                <div class="ansibleOptionAnchor" id="parameter-local_pkgbuild"></div>
                <b>local_pkgbuild</b>
                <a class="ansibleOptionLink" href="#parameter-local_pkgbuild" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">path</span>
                                                                </div>
                                                    </td>
                            <td>
                                                                                                                                                                                                            <b>Default:</b><br/><div style="color: blue">"no"</div>
                                </td>
                                                            <td>
                                        <div>Local directory with PKGBUILD and build files. Only supported with makepkg or pikaur. Cannot be used unless use is set to &#x27;makepkg&#x27; or &#x27;pikaur&#x27;.</div>
                                                    </td>
        </tr>
                            <tr>
                                                            <td colspan="1">
                <div class="ansibleOptionAnchor" id="parameter-name"></div>
                <b>name</b>
                <a class="ansibleOptionLink" href="#parameter-name" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">string</span>
                                                                </div>
                                                    </td>
                            <td>
                                                                                                                                                        </td>
                                                            <td>
                                        <div>Name or list of names of the package(s) to install or upgrade.</div>
                                                    </td>
        </tr>
                            <tr>
                                                            <td colspan="1">
                <div class="ansibleOptionAnchor" id="parameter-skip_pgp_check"></div>
                <b>skip_pgp_check</b>
                <a class="ansibleOptionLink" href="#parameter-skip_pgp_check" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">boolean</span>
                                                                </div>
                                                    </td>
                            <td>
                                                                                                                                                                                                                <ul style="margin: 0; padding: 0"><b>Choices:</b>
                                                                                                                                                            <li><div style="color: blue"><b>no</b>&nbsp;&larr;</div></li>
                                                                                                                                                                                            <li>yes</li>
                                                                                </ul>
                                                                        </td>
                                                            <td>
                                        <div>Only supported with makepkg. Skip PGP signatures verification of source file. This is useful when installing packages without GnuPG configured properly.</div>
                                                    </td>
        </tr>
                            <tr>
                                                            <td colspan="1">
                <div class="ansibleOptionAnchor" id="parameter-state"></div>
                <b>state</b>
                <a class="ansibleOptionLink" href="#parameter-state" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">string</span>
                                                                </div>
                                                    </td>
                            <td>
                                                                                                                        <ul style="margin: 0; padding: 0"><b>Choices:</b>
                                                                                                                                                            <li><div style="color: blue"><b>present</b>&nbsp;&larr;</div></li>
                                                                                                                                                                                            <li>latest</li>
                                                                                </ul>
                                                                        </td>
                                                            <td>
                                        <div>Desired state of the package; &#x27;present&#x27; skips operations if the package is already installed.</div>
                                                    </td>
        </tr>
                            <tr>
                                                            <td colspan="1">
                <div class="ansibleOptionAnchor" id="parameter-upgrade"></div>
                <b>upgrade</b>
                <a class="ansibleOptionLink" href="#parameter-upgrade" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">boolean</span>
                                                                </div>
                                                    </td>
                            <td>
                                                                                                                                                                                                                <ul style="margin: 0; padding: 0"><b>Choices:</b>
                                                                                                                                                            <li><div style="color: blue"><b>no</b>&nbsp;&larr;</div></li>
                                                                                                                                                                                            <li>yes</li>
                                                                                </ul>
                                                                        </td>
                                                            <td>
                                        <div>Whether or not to upgrade whole system.</div>
                                                    </td>
        </tr>
                            <tr>
                                                            <td colspan="1">
                <div class="ansibleOptionAnchor" id="parameter-use"></div>
                <b>use</b>
                <a class="ansibleOptionLink" href="#parameter-use" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">string</span>
                                                                </div>
                                                    </td>
                            <td>
                                                                                                                        <ul style="margin: 0; padding: 0"><b>Choices:</b>
                                                                                                                                                            <li><div style="color: blue"><b>auto</b>&nbsp;&larr;</div></li>
                                                                                                                                                                                            <li>yay</li>
                                                                                                                                                                                            <li>paru</li>
                                                                                                                                                                                            <li>pacaur</li>
                                                                                                                                                                                            <li>trizen</li>
                                                                                                                                                                                            <li>pikaur</li>
                                                                                                                                                                                            <li>aurman</li>
                                                                                                                                                                                            <li>makepkg</li>
                                                                                </ul>
                                                                        </td>
                                                            <td>
                                        <div>The AUR helper to use. &#x27;auto&#x27; uses the first known helper found or &#x27;makepkg&#x27; as a fallback.</div>
                                                    </td>
        </tr>
                    </table>
<br/>
