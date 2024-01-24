Acoustic Modems
###############

Time definitions
================

.. list-table:: 
   :header-rows: 1
   :align: center

   * - Variable
     - Description

   * - :math:`T_{\text{p}}`
     - Poll duration
   * - :math:`\tau_{\text{p}}`
     - Propagation delay (travel time of poll)
   * - :math:`T_{\text{wp}}`
     - Processing delay receiver (process poll, generate response and switch from receiving to transmission mode)
   * - :math:`T_{\text{r}}`
     - Response duration
   * - :math:`T_\text{TWR}`
     - Measured two-way-ranging time, with :math:`T_\text{TWR} = t_\text{r} - t'_\text{p}` 
   * - :math:`\tau`
     - Time of flight (TOF), with :math:`\tau = \frac{T_\text{TWR} - T_\text{wp}}{2} = \frac{\tau_\text{p} + \tau_\text{r}}{2}` 
   * - :math:`T_\text{wr}`
     - Processing delay agent
   * - :math:`\tau_\text{r}`
     - Travel time of response


**Broadcast algorithm**: Single broadcast poll packet from agent, which is received by all anchors. 
Responses are transmitted sequentially, implemented e.g. by using different :math:`T_{\text{wp},i}` for each anchor :math:`i`. 
Unique offset :math:`T_{\text{wp},i}` is called *ranging delay*.

**Alternating algorithm**: Send individual poll to each anchor



